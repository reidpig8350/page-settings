---
title: "【Python】更新資料庫狀態"
date: 2022-02-10
draft: 0

# post thumb
image: ""

# meta description
description: "Google Cloud Platform, Bigquery, Google Cloud Storage, SQL, Merge, "

# taxonomies
categories:
  - "Google & Python"
tags:
  - "Python"
  - "Google Sheets"
  - "串接Google Sheets"


# post type
type: "featured"
---

>Upsert 功能是兩個概念所組成的複合字，包含了更新 (Update) 以及 插入 (Insert)，是管理資料庫時的重要概念。以下舉 [BigQuery](https://zh.wikipedia.org/wiki/BigQuery "BigQuery
") 為例，示範如何以 SQL 語言完成 Upsert 管理資料庫
<!--more-->

#### Google Cloud Platform (GCP)
[Google Cloud Platform](https://console.cloud.google.com/?hl=zh-TW "Google Cloud Platform") (GCP) 是管理 Google 產品的平台，就像是 Amazon 的 [AWS](https://en.wikipedia.org/wiki/Amazon_Web_Services "Amazon 雲端服務平台") 以及 Microsoft 的 [Azure](https://zh.wikipedia.org/wiki/Microsoft_Azure "Microsoft 雲端服務平台")，而 GCP 即是整合 Google 雲端服務的平台。

在日常的娛樂以及工作的應用程式，Google 在各方面都已經是不可或缺的角色，只要你能夠在 Google 首頁找得到的應用程式，都可以在 GCP 中找到**相應的 API**。Gmail、Google Maps、Google Document 或者 Google Drive 等等，當你有自動化或者研發的需求時，都必須接觸 [Google Cloud Platform](https://console.cloud.google.com/?hl=zh-TW "Google Cloud Platform") 找到相應的服務。

#### Scenario
在行銷市場中，有許多針對促銷訊息設計的系統，以 email 促銷為例（EDM, Eletronic Direct Mail)。當你想要追蹤發出的 EDM 是否有經歷你所期待的歷程收到信件並活動訊息：

**發信&rarr;開信&rarr;點擊信中活動連結**，代表資料庫中**訊息的狀態需要被更新**。

以上述的情境為例，當新的促銷訊息產生時必須判斷資料庫中是否已經有資料：
* 若有資料則更新 EDM 狀態 (**Update**)
* 若無資料則插入新的一列 (**Insert**)

#### Practice

接下來以實際的資料作為範例，資料的最後一欄 (status) 代表**追蹤狀態**，顯示 EDM **目前**的狀態為何。

###### EDM 所經歷的歷程可以拆解成以下三個步驟：
1. sent: 成功寄出信件
1. open: 打開信件
1. click: 點擊連結

|system_id|promotion|event|status|
|-----|-----|-----|-----|
|KK-0002052954|[EDM]|Reminder_ZH|sent|
|KK-0002052947|[EDM]|Reminder_ZH|sent|
|KK-0002052977|[EDM]|Reminder_ZH|open|
|KK-0002052974|[EDM]|Reminder_ZH|click|
|KK-0002052971|[EDM]|Reminder_ZH|click|

因此每當資料更新狀態，也必須依據 Primary Key (這筆資料以 system_id 作為 Primary Key)更新信件的狀態。

#### Programming

由於 SQL 並沒有直接的 Upsert 指令可以更新狀態，因此必須 MERGE 更新前後的兩張表格，並且以 system_id 作為查找依據。


```SQL
    MERGE
        project_name.client_list.promotion_edm T
    USING
        project_name.client_list_records.promotion_edm_today S
    ON
        T.system_id = S.system_id
        WHEN NOT MATCHED THEN INSERT (`system_id`, `sent_date__c`, `content_name__c`, `journey_content__r_a_b_test__c`, `type__c`, `card_no__c`, `card_type__c`, `status__c`, `arrival_station__c`, `departure_station__c`, `pnr_number`, `utm_content__c`, `birthday_event_date`) VALUES (`system_id`, `sent_date__c`, `content_name__c`, `journey_content__r_a_b_test__c`, `type__c`, `card_no__c`, `card_type__c`, `status__c`, `arrival_station__c`, `departure_station__c`, `pnr_number`, `utm_content__c`, `birthday_event_date`)
        WHEN MATCHED
        THEN
    UPDATE
    SET
        status__c=S.status__c;
```

除了 Database 以及 Table，BigQuery 還需要在指定 Table 時指出是「哪一個專案」。因此在對應 Project Name 下再以點號指明 database.table。

MERGER 指出**被更新的Table**，USING 則是**新狀態的表格**，條件則是 ON system_id (Primary ID) 將相同的資料更新。
Primary Key 不符合 (NOT MATCHED)時，代筆這筆資料是全新的資訊，因此需要直接插入 INSERT；Primary Key 符合 (MATCHED)則將 EDM 的狀態更新 UPDATE SET 更新資料。
