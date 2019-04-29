---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

subcollection: tone-analyzer

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# 服務背後的科學
{: #ssbts}

{{site.data.keyword.toneanalyzerfull}} 服務是以心理語言學的理論為基礎，這是一種探索語言行為與心理理論之間關係的研究領域。此服務會使用語言分析及撰寫文字語言特性與情緒和語言語氣之間的相關性，為其中每一種語氣維度制定評分。
{: shortdesc}

心理語言學研究員致力於瞭解人員日常生活中所使用的單字是否反映出他們的身分、感受及思考方式。在經過數十年的研究之後，現在心理學、市場行銷及其他領域都已接受下列觀點：語言不僅僅反映出人員想說的內容。人員使用特定類型單字的頻率可以提供人格特質、思考型態、社交關係及情緒狀態的線索。

例如，人們在其日常溝通中表現出各種語氣：愉快或悲傷、開放或保守、善於分析或不拘小節（[Gou 等人，2014](/docs/services/tone-analyzer?topic=tone-analyzer-references#bib-gou) 及 [Jian 等人，2014](/docs/services/tone-analyzer?topic=tone-analyzer-references#bib-jian)）。這些語氣會影響個人線上身分的認知，以及他們在不同環境定義中的溝通成效。

此外，在商業電子郵件通訊中，人們可能會比正面情緒更強烈地感受到負面情緒（[Byron，2008](/docs/services/tone-analyzer?topic=tone-analyzer-references#bib-byron)）。而在社群媒體中，人們所呈現的不同線上身分會影響其他人對其所擁有的印象（[DiMicco 及 Millen，2007](/docs/services/tone-analyzer?topic=tone-analyzer-references#bib-dimicco)）。

許多人會自然地閱讀訊息，並判斷寄件者所傳達的語氣。但是電腦可以正確且自動地偵測訊息所顯露的語氣嗎？此問題是人工智慧和認知科學領域中的研究人員正在尋求答案的許多挑戰性問題之一。在最早具備 {{site.data.keyword.personalityinsightsshort}} 服務而現在有了 {{site.data.keyword.toneanalyzershort}} 服務的情況下，IBM 將會回答這個問題。

## 相關研究的概觀
{: #sorr}

研究表明在單字選擇與人格特質、情緒、態度、內在需求、價值觀及思考過程之間具有統計意義的高度相關性。有些研究人員發現，人們在撰寫部落格、散文及推文時，使用某些種類單字的頻率會有所不同。研究人員發現下列溝通手段可以協助預測人格特質的不同層面：

-   [Fast 與 Funder (2008)](/docs/services/tone-analyzer?topic=tone-analyzer-references#bib-fast)
-   [Gill 等人 (2009)](/docs/services/tone-analyzer?topic=tone-analyzer-references#bib-gill)
-   [Golbeck 等人 (2011)](/docs/services/tone-analyzer?topic=tone-analyzer-references#bib-golbeck)
-   [Hirsh 與 Peterson (2009)](/docs/services/tone-analyzer?topic=tone-analyzer-references#bib-hirsh)
-   [Yarkoni (2010)](/docs/services/tone-analyzer?topic=tone-analyzer-references#bib-yarkoni)

大部分的上述工作都是基於從寫作的單字用法來尋找心理學上有意義的單字種類。此研究是作為 IBM 在 {{site.data.keyword.toneanalyzershort}} 服務上的工作基礎。根據心理語言學研究的科學成果，IBM 致力於從人們所寫的字推斷他們的人格特質、思考型態與寫作風格、情緒，以及內在需求和價值觀。IBM 會使用其機器學習模型，透過評量人員寫作的各種特性來評估這些特質。

## 一般用途模型
{: #analysis}

一般用途端點會針對一組適用於廣泛用途的語氣分析撰寫內容。{{site.data.keyword.toneanalyzershort}} 服務會計算包含下列語氣的計分卡：

-   **情緒語氣**是衍生自 IBM 在情緒分析上的工作，這是一種可從文字推斷情緒的集合架構。為了從文字衍生情緒評分，IBM 會使用堆疊一般化型集合架構；堆疊一般化則使用高階模型來結合低階模型，以達到更高的預測精確度。諸如 n-gram（unigram、bigram 及 trigram）、標點符號、表情符號、咒罵語、問候語（例如 "hello"、"hi" 及 "thanks"）及觀感極性之類的特性，都會送入機器學習演算法來分類情緒種類。
-   **語言語氣**是根據學習的特性從語言分析計算而來。

### 測量服務的品質
{: #smqs}

IBM 已根據上節的語氣維度測量 {{site.data.keyword.toneanalyzershort}} 服務的品質：

-   *情緒語氣*種類已針對標準情緒資料集（例如 ISEAR 及 SEMEVAL）進行基準性能測試。結果顯示集合模型的平均效能（這兩個資料集的巨集平均 F1 評分大約為 41% 及 68%）在統計上優於最先進模型的最佳報告精確度（其巨集平均 F1 評分分別大約為 37% 及 63%）。
-   *語言語氣* 已透過深入研究收集自來源（例如辯論討論區、演說及社交媒體）的兩百萬以上句子來進行評估。IBM 已針對善於分析語氣隨機選取 1330 個句子，並針對自信和猶豫語氣各選取 1000 個句子。然後，IBM 會將句子提交給 {{site.data.keyword.toneanalyzershort}} 服務，並要求人們分析這些句子。

    IBM 在人工分析方面，使用了稱為 [CrowdFlower ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.crowdflower.com/){: new_window} 的群眾外包平台，以不同的標籤來標註所選取的句子。只有核准率超過 85% 的評比者才能參與註釋作業。有五位標註者標示每個句子，IBM 則使用最常見的五個標註結果來決定最終的標籤。
    -   對於*善於分析語氣*，人們已將 1330 個句子中的 915 句標示為善於分析，411 句標示為不善於分析，而 4 句標示為無法理解。透過比較預測的標籤與這些基準 (ground-truth) 標籤，IBM 發現其善於分析語氣偵測得到 F1 評分 0.7518。
    -   對於*猶豫語氣*，人們已將 1000 個句子中的 292 句標示為猶豫，706 句標示為不猶豫，而 2 句標示為無法理解。透過比較預測的標籤與基準標籤，IBM 發現其猶豫語氣偵測得到 F1 評分 0.6369。
    -   對於*自信語氣*，人們已將 1000 個句子中的 623 句標示為自信，374 句標示為不自信，而 3 句標示為無法理解。透過比較預測的標籤與基準標籤，IBM 發現其自信語氣偵測得到 F1 評分 0.7288。

整體而言，預測的標籤與基準標籤之間的差異在統計上並不重要。此結果表示服務執行狀況良好。

## 客戶參與模型
{: #scem}

客戶參與端點可從客戶關懷領域識別語氣。為了選取要使用客戶參與模型評估的語氣，IBM 已先進行一項研究，以識別在該領域中哪些語氣維度被認為重要：

1.  IBM 從市場行銷中使用的維度、用來說明寫作風格的維度以及心理學的情緒和人格特質量表中選取一組 53 種語氣。
1.  IBM 要求 CrowdFlower 的工作者評比 53 種語氣屬性在 1000 個客戶關懷交談中描述特定陳述的程度。為了簡化群眾外包環境定義中的評等作業，IBM 已將 53 種語氣分成四個子集。註釋人員只需評比某個語氣子集。IBM 接著會從這些結果的彙總中判定所有語氣的評等。
1.  IBM 對一個 53x53 相關性矩陣執行了因素分析，找到至少七個重要因素（維度）。IBM 已判定因素名稱，用來代表每一個維度所反映的最重要概念。

這些步驟會針對客戶關懷領域，識別出七個重要語氣維度：frustration、satisfaction、excitement、politeness、impoliteness、sadness 及 sympathy。

### 資料收集
{: #sdc}

IBM 使用 Twitter 客戶支援討論區作為交談式資料的來源，以在客戶關懷領域中進行語氣分析。許多公司使用 Twitter 作為通道，以提供其客戶支援。雇用並訓練客服人員，以監視提及公司的推文、指導協助要求，以及提供快速支援來處理客戶的需求。

為了盡可能多收集交談，IBM 已選取 62 個在 Twitter 上具有專用客戶服務帳戶的品牌。IBM 選擇這些品牌來涵蓋各種產業、地理位置，以及組織規模。整體而言，IBM 在 2016 年 6 月 1 日到 8 月 1 日之間收集了 260 萬個使用者要求。

### 資料註釋
{: #sda}

IBM 已過濾收集的資料集，只保留至少收到一則回覆，而且只涉及一個客戶及一個客服人員的那些交談。IBM 還會從資料集中移除所有非英文交談，以及包含的要求或答案具有影像的交談。為了保護使用者和公司的隱私權，IBM 已將每一個交談中的所有 *@mentions* 取代為 *@customer*、*@[industry]_company*（例如 *@ecommerce_company* 或 *@telecommunication_company*）、*@competitor_company* 或 *@other_users*。

這項選擇處理識別出大約 96000 個交談陳述要由 CrowdFlower 工作者進行標註。為了進一步瞭解註釋上下文，IBM 已要求工作者在交談層次上進行標註，並標示交談中涉及的所有陳述。某些所提出語氣的主觀本質可能會導致認知不一致。因此，IBM 會要求註釋人員根據具有四個點的李克特量表（範圍從「非常強烈」到「完全不強烈」），指出他們感覺該陳述表現出語氣的強烈程度。李克特量表比簡單的二元是/否量表更適用，因為它對於各種認知可容納較高的容錯，並產生較少稀疏的標籤。

有五位不同的標註者標示每個交談。IBM 只會使用設籍美國且之前的註釋作業達到可接受之績效層次的標註者。此外，IBM 還需要標註者正確回答五個訓練問題，才能繼續進行實際的註釋作業。這些訓練問題可確保標註者了解每種語氣在客戶服務環境定義中的意義。IBM 還會在實際作業中內含驗證問題，以進一步驗證標註者的標籤品質。

IBM 會使用五位標註者的評分平均值作為每個陳述的最終標籤。接著，IBM 會使用評分 1 作為將標籤轉換為二進位值的臨界值。IBM 根據對標籤分佈的觀察以及具有不同臨界值之模型的效能，選擇 1 作為臨界值。最終結果是產生下列的陳述分佈：9536 個挫敗、10,806 個滿意、6107 個興奮、63,853 個有禮貌、1688 個沒有禮貌、24,954 個悲傷，以及 10,475 個同情。

### 學習語氣模型
{: #sltm}

根據這些客戶參與交談，IBM 已基於「支援向量機器 (SVM)」來訓練機器學習模型，以預測新的客戶關懷陳述的語氣。對於機器學習模型，IBM 已利用數種種類的特性：

-   n-gram 特性
-   各種字典中的詞彙特性
-   交談中存在第二位人員參照
-   部分對話特定特性，例如說出謝謝您或抱歉
-   數個較高階特性，例如存在連續問號或驚嘆號

IBM 發現大約有 30% 的範例具有多個相關聯的語氣。因此，IBM 選擇解決多標籤分類作業，而非多類別分類作業。對於每一種語氣，IBM 都會使用 One-vs-Rest (OVR) 參照範例來獨立訓練模型。參照範例會使用每一個類別的陳述作為正面範例，並使用所有其他陳述作為負面範例。IBM 將預測至少有 0.5 機率的語氣識別為最終語氣。對於幾種語氣來說，訓練資料嚴重失衡；因此，IBM 已在訓練期間為每種語氣識別出成本函數的最佳權重值。

IBM 已使用精準度、查全率及 F 評分，以評估其分類模型的精確度。相較於基準性能測試資料集，模型具有高精確度。
