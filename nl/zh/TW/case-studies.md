---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

subcollection: tone-analyzer

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 個案研討
{: #caseStudies}

請閱讀這些個案研討，以瞭解您可以使用 {{site.data.keyword.toneanalyzerfull}} 服務執行的作業。這些研討說明所描述的語氣與預期成果之間的相關性。相關性可以是正值或負值，範圍為 -1.0 到 1.0。
{: shortdesc}

## 預測支援討論區的客戶滿意度
{: #supportForums}

IBM 已針對一個以多個產業為主的軟體公司分析了客戶支援討論區。該公司積極參與客戶支援討論區。使用者可以對他們發現有用的答案給讚 (*Kudo*)。

### 目標
{: #supportForumsGoals}

從問題和回應的語氣預測客戶滿意度。IBM 假設具有讚的答案表示使用者感到滿意。

### 動作
{: #supportForumsActions}

-   已搜索數個討論區中最新的 1000 個討論串，並確定要包含相同數目的含讚回應與不含讚回應。
-   已同時分析問題及回應。
-   已套用數個最先進的分類器（例如單純貝氏、「支援向量機器 (SVM) 」及隨機森林），以預測答案是否會獲得讚。

### 結果
{: #supportForumsResults}

服務預測讚的正確度 可以達到 66%。IBM 在討論區回應的語氣與該回覆是否獲得讚之間，發現下列相關性：

-   回應越有自信，贏得讚的可能性就越大（自信的高值評分與讚的相關性為 0.23）。
-   回應越猶豫，贏得讚的可能性就越小（猶豫的高值評分與讚的負相關性為 -0.27）。

## 預測 Twitter 回應的客戶滿意度
{: #twitterResponses}

許多公司正在將其客戶支援轉向Twitter。Twitter 可容許即時回答，這有助於將品牌建立為有真人關懷客戶的品牌。

IBM 已在 Twitter 上分析 333 則客戶支援交談。客戶對其中 240 則交談感到滿意，對其中 93 個互動感到不滿意。IBM 已透過閱讀交談並將其加上標籤來測量滿意度。當他們解決了問題而客戶似乎感到滿意時，回應會標示「客戶滿意」。當問題未解決而無法讓客戶滿意時，會標示「客戶不滿意」。

### 目標
{: #twitterResponsesGoals}

驗證客服人員與客戶之間的交談語氣是否影響整體客戶滿意度。同時也會識別顯著影響客戶滿意度的語氣。

### 動作
{: #twitterResponsesActions}

-   已從推文中刪去標點符號、提及項目及鏈結。
-   已將每個互動分割為客戶推文和支援人員推文。
-   已使用 {{site.data.keyword.toneanalyzershort}} 服務分析交談的每一端，並比較結果以找出相關性。

### 結果
{: #twitterResponsesResults}

服務從回應的語氣預測客戶滿意度，正確度 可以達到 67%。IBM 在客戶推文的語氣與客戶是否滿意回應之間，發現下列相關性：

-   客戶越生氣，他們對回應感到滿意的可能性就越低。客戶推文的生氣高值評分與客戶滿意度之間的負相關性為 -0.198。

## 預測 TED 演講掌聲
{: #tedTalks}

TED 是非營利性組織，以標語 "Ideas worth spreading" 來策劃全球會議。TED 演講者有 18 分鐘，可使用創新及吸引人的說故事方法，發表與科學和文化的研究及實踐相關的廣泛主題。並非所有 TED 演講都廣受歡迎，其中一種測量演講聽眾滿意度的方法是測量所獲得掌聲的數量。

### 目標
{: #tedTalksGoals}

探索 TED 演講中的哪些語氣模式會引來掌聲，而哪些模式不會。同時也根據句子的語氣來預測掌聲。

### 動作
{: #tedTalksActions}

已在資料集中標記獲得掌聲的句子。

-   已檢閱 1931 場 TED 演講。
-   已將標記為 "Applause" 的句子分類為「掌聲文字」。此外，已將該句子前面的三個句子標記為「掌聲文字」，並將其之後的三個句子標記為「非掌聲文字」。
-   已使用 {{site.data.keyword.toneanalyzershort}} 服務分析掌聲及非掌聲文字。
-   根據發現的相關性，已建立分類器，以根據其他 TED 演講的語氣來預測其中的掌聲。

### 結果
{: #tedTalksResults}

服務預測掌聲的正確度 可以達到 75%。IBM 在每組句子的語氣與這些句子是否獲得掌聲之間，發現下列相關性：

-   演講者表現得越悲傷，他們獲得掌聲的可能性就越低（悲傷的高值評分與掌聲之間的負相關性為 -0.055）。
-   演講者看起來越無情或冷淡，他們獲得掌聲的可能性就越低（善於分析的高值評分與掌聲之間的負相關性為 -0.29）。
-   演講者看起來越愉快、知足及滿意，他們獲得掌聲的可能性就越高（愉快的高值評分與掌聲之間的相關性為 0.21）。

## 預測 Twitter 推文及按讚
{: #twitterRetweets}

在 Twitter 上建立品牌逐漸變成公司要成功的一項要求。將您或您的公司建立為值得關注，有一個重要的部分是在於建立獲得許多按讚及轉推的推文。

### 目標
{: #twitterRetweetsGoals}

找出推文的語氣與該推文是否獲得按讚或轉推之間的相關性。

### 動作
{: #twitterRetweetsActions}

-   已在 Twitter 上的數個商業帳戶中搜索 5881 則推文。
-   已從推文中刪去標點符號、提及項目及鏈結。
-   使用 {{site.data.keyword.toneanalyzershort}} 服務分析每一則推文，並比較結果以找出相關性。

### 結果
{: #twitterRetweetsResults}

IBM 在推文的語氣與推文是否獲得按讚之間，以及推文的語氣與推文是否獲得轉推之間，發現下列相關性。

## 預測線上約會配對者
{: #onlineDating}

世界各地數以百萬的人使用線上約會來認識那個特殊的人。人們使用線上約會來尋找與他們有許多共同點的其他人，並行銷自已作為潛在的夥伴。

### 目標
{: #onlineDatingGoals}

將個人人員資訊的語氣與潛在配對者的人員資訊語氣產生關聯。同時也探索該相關性是否預測配對成功。

### 動作
{: #onlineDatingActions}

-   已搜索大約 50,000 份使用者人員資訊。
-   已使用 {{site.data.keyword.toneanalyzershort}} 服務分析每份人員資訊。
-   已將潛在配對者定義為透過該網站進行溝通的使用者。
-   已比較潛在配對者的語氣分析以找出相關性。
-   已從人員資訊的語氣相似性開發出一個統計模型，用來預測兩個使用者是否會進行溝通。然後，將模型與考量其他屬性（例如個人背景資訊）的多個基準線進行比較。

### 結果
{: #onlineDatingResults}

相較於約會網站經常使用的預測工具，人員資訊之間的語氣相似性在預測兩個使用者是否進行溝通方面改善了 45%。IBM 在語氣相似性與交流的訊息數目之間發現高度相關性，如下圖所示。

![分析的語氣與交流的訊息數目之間的高度相關性。](images/case-study.svg)
