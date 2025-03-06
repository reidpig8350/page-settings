---
author: "Reid"
title: "如何用 GTM 設定 GA4 事件"
date: "2025-02-22"
description: "以瀏覽事件為例，利用 GTM 快速設定 GA4 事件，精準追蹤使用者行為。"
tags: ["GA4", "GTM"]
categories: ["GA4", "事件追蹤"]
series: ["GA4 教學"]
images: ["/images/ga4-blue.jpeg", "/images/hero-image.png"]
---
在 GTM 中設定 GA4 事件非常直觀。首先，進入 GTM 後新增「Google Analytics: GA4 事件」標籤，並綁定您的 GA4 設定碼。以瀏覽事件為例，請將事件名稱設定為 `page_view`，並於事件參數中填入頁面標題、URL 等關鍵數據。隨後，建立一個觸發器，建議設為所有頁面載入時自動啟動，或根據需求指定特定頁面。啟用預覽模式後，確認標籤正確觸發並將數據傳送至 GA4，再檢視數據是否完整呈現。確認測試無誤後，即可提交發布。透過此流程，您能精準追蹤瀏覽行為，進而優化網站設計與行銷策略。