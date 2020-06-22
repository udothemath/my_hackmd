# 數位貸款 CFT x 產學合作
###### tags: `info` `note`
---

::: info

### 專案參與人員
- 中研院：王釧茹老師、匡顯吉、張嘉元、簡伯銓
- 玉山銀行：施晨揚經理、葉倚任副理、孫甫璋、蒲冠吉、陳品瑜

### 時程 
```mermaid
gantt
dateFormat  YYYY-MM-DD
axisFormat %-m/%-d
title Project Progress

section Model Phase 1
The Coming Meeting?:active, des5, 2020-07-13, 2020-07-28
Next Meeting?:active, des4, 2020-06-22, 2020-07-13
Model Discussion:done, des3, 2020-05-25, 4w
Data Discussion:done, des2, 2020-05-04, 3w
Kick-off:done, des1, 2020-04-27, 1w
section Model Phase 2
End_of_2020:active,  des2, 2020-12-15, 2w
```
### 討論管道
- [This HackMD](https://hackmd.io/UAZjUsvnQSKARtNsiKIgGQ?view)
- [Slack](https://cfda-clip.slack.com/#/)
- Google Meet: Next meeting invitation is provided at the end of the discussion 

### 會議紀錄
- [Latest Meeting](##Meeting)
- [5/25 Data discussion](##5/25/2020_3-4pm)
- [5/4 Kick-off](##5/4/2020_3-4pm)
:::

---
## Meeting

## 6/22/2020 3-4PM
### 與會人
- 中研院：王釧茹老師、匡顯吉、張嘉元、簡伯銓
- 玉山銀行：甫璋、冠吉、品瑜(會議記錄)

### ToDo
|參與人員|信箱|
|--|--|
|王釧茹老師|jerewang@gmail.com|
|匡顯吉|10832502@mail2.nccu.tw|
|張嘉元|z7631614@gmail.com|
|簡伯銓|bor810818@yahoo.com.tw|
|施晨揚經理|kentesuntw@gmail.com|
|葉倚任副理|yirenyeh@gmail.com|
|孫甫璋|fuchang.sun@gmail.com|
|蒲冠吉|pontussecret@gmail.com|
|陳品瑜|pypychen@umich.edu|

### Recap
> 在Google(or Facebook)廣告通路上，提供曾經瀏覽過玉山網頁的顧客所需要的產品/服務。現行的廣告投放名單篩選機制是根據顧客的網頁瀏覽行為，透過人工定義的條件篩選得出，惟此方法的篩選機制需要人工判斷，此專案希望可以藉由機器學習方法，降低人工調整名單的成本，提升名單轉換率，並發現活躍顧客的重要特徵。
### 目標
- 提升名單轉換率
- 活躍顧客的重要特徵

### 今日議程
#### 方法討論
1. [瀏覽器cookie特性](https://datastudio.google.com/u/0/reporting/2e6c7be5-764c-4641-a8e3-27617321937a/page/3wsSB)
1. 模型: 協同過濾方法(Collaborative filtering)
    - ![](https://i.imgur.com/DbyxCqq.jpg)
1. 驗證方法: precision, recall, (or [MAP@N, mean average precision @ N](https://medium.com/@bond.kirill.alexandrovich/precision-and-recall-in-recommender-systems-and-some-metrics-stuff-ca2ad385c5f8) )
1. 資料處理:
    - 資料分割: 過去__天的URL造訪紀錄(建議短天期: 3-7天)，預測未來7天是否造訪產品申請頁面
    - 目前規劃僅使用短天期的網頁瀏覽行為建模的兩個原因如下
        - 瀏覽器cookie容易失效的特性
        - 藉由資料EDA以及業務的了解，顧客通常會在短時間即有信貸/卡友貸的需求
1. 建模進度分享:
- 案例設定
<table>
    <thead>
        <tr>
            <th>Case</th>
            <th>Training</th>
            <th>Keywords in targeting URL</th>
            <th>Number of record</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td> 1 </td>
            <td rowspan=3>4/1-4/7</td>
            <td rowspan=1>模型A: loan, Loan</td>
            <td rowspan=3>500, 1000, 2000</td>
        </tr>
        <tr>
            <td> 2 </td>
            <td rowspan=1>模型B: /s/PersonalLoan, /EsunCreditweb/txnservice</td>
        </tr>
        <tr>
            <td> 3 </td>
            <td>模型C: 同模型B，interaction matrix負數改成0</td>
        </tr>
        <tr>
            <td> 4 </td>
            <td rowspan=3>4/1-4/14</td>
            <td rowspan=1>模型A: loan, Loan</td>
            <td rowspan=3>1000, 3000, 5000</td>
        </tr>
        <tr>
            <td> 5 </td>
            <td rowspan=1>模型B: /s/PersonalLoan, /EsunCreditweb/txnservice</td>
        </tr>
        <tr>
            <td> 6 </td>
            <td>模型C: 同模型B，interaction matrix負數改成0</td>
        </tr>
        <tr>
            <td> 7 </td>
            <td rowspan=3>4/1-4/21</td>
            <td rowspan=1>模型A: loan, Loan</td>
            <td rowspan=3>1000, 3000, 5000</td>
        </tr>
        <tr>
            <td> 8 </td>
            <td rowspan=1>模型B: /s/PersonalLoan, /EsunCreditweb/txnservice</td>
        </tr>
        <tr>
            <td> 9 </td>
            <td>模型C: 同模型B，interaction matrix負數改成0</td>
        </tr>
    </tbody>
</table>

- 初步結論:
    - 模型結果: C > B > A 
    - 觀測區間3-7日即可
- 成效比較:
    - [Precision and Recall with Details](https://esgarden.esunbank.com.tw/personal/esb20033/_layouts/15/WopiFrame.aspx?sourcedoc={7BB5C80A-0D6D-4C85-827C-D15BB348CB7C}&file=%E8%B2%B8%E6%AC%BE%E7%94%A2%E5%AD%B8%E5%90%88%E4%BD%9C%20%20baseline.docx&action=default)
- 基本EDA:
    - [2020 4月 每日y1 y0人數](https://esgarden.esunbank.com.tw/personal/esb20033/Documents/cft_loan/202004_y1y0_byDate.png)

### 會議記錄
#### Baseline Model:
* Rule Based:
    * 瀏覽紀錄 >= 5筆, y=1
    * 在target頁前瀏覽紀錄 >= 4筆, y=1
* Logistic Regression:
    * 取每個clientID最長的session代表此用戶
    * session的最後一頁視為該用戶的目標頁
    * 類別變數做one-hot-encoding
    * 約莫10個variables
    * Precision > 0.99
* ToDo: 扣掉y=1當天和前一天的瀏覽紀錄，retrain模型
* [中研院簡報檔](!https://docs.google.com/presentation/d/191_9NhYNO-X6OCMqyBg-49Ahstc5RW4LL7oIWUYhkxQ/edit?usp=sharing)

### 待辦
- 調整權限
- 下次會議時間
- 下次討論內容

## 5/25/2020_3-4pm
### 與會人
- 中研院：王釧茹老師、匡顯吉、張嘉元、簡伯銓
- 玉山銀行：晨揚經理、倚任副理、甫璋、冠吉(會議記錄)、品瑜

### 今日議程
1. 建模資料討論
    - [Brief EDA](https://datastudio.google.com/reporting/2e6c7be5-764c-4641-a8e3-27617321937a)
1. 建模方法討論
### 待辦
1. 下次會議時間:
    - 2020-06-22 3-4pm
1. 下次報告形式與內容
    - TBD
1. 跟CFT確認幾天給一次名單合適，模型預測幾天內會購買?
    - (原訂30天，但需要再討論業務場景)
1. USER id多久會回訪?
    - 請參考資料源
1. 這幾個月Y的分布是不是一樣?
    - 是，分布情況雷同
1. 確認ID對不上的情況
    - 確認ID無誤
1. TRAIN-TEST split、baseline
    - TBD

### 與會人
- 中研院：王釧茹老師、匡顯吉、張嘉元、簡伯銓
- 玉山銀行：晨揚經理、倚任副理、甫璋、冠吉(會議記錄)、品瑜

### 會議記錄
1. 確認有下載資料權限
1. y=1是4月，建模的資料不可以用到，實用是多久更新一次，幾天給名單?需再跟業管單位確認
    - 現行是每天以rule-based的方法產製名單
1. 只用4月當Y=1會不會bias?
    - 不會。2020年，1-4月資料樣貌雷同(https://datastudio.google.com/reporting/2e6c7be5-764c-4641-a8e3-27617321937a)
1. 瀏覽紀錄的次數(每個ID看過幾頁)也許是個強特徵
1. 有2筆特別的id格式，刪除。
1. 7z、gzip壓縮
1. 模型預想：以頁面為端點、一定時間內同時看過連線(Network)；end to end binary classification

## 5/4/2020_3-4pm
### 與會人
- 中研院：王釧茹老師、匡顯吉、張嘉元、簡伯銓
- 玉山銀行：晨揚經理、倚任副理、甫璋、冠吉、品瑜(會議記錄)

### 今日議程
1.	專案簡介(introduction)
2.	專案目標(objectives)
3.	衡量標準(metrics)
4.	現有模型成效(if any, current model performance)
5.	資料來源(data resource)
6.	會議規劃(meeting schedule)
7.	討論(discussion)

### 專案簡介
> 在Facebook廣告通路上，提供曾經瀏覽過玉山網頁的顧客所需要的產品/服務。現行的fb投放名單篩選機制是根據顧客的網頁瀏覽行為，透過人工定義的條件篩選得出，惟此方法的篩選機制需要人工判斷，此專案希望可以藉由機器學習方法，降低人工調整名單的成本，提升名單轉換率，並發現活躍顧客的重要特徵。

### 專案目標
藉由機器學習模型(方法不限)，產出信貸以及卡友貸合適的行銷名單，定義合適的衡量標準，追蹤模型成效。

舉例：
現行的篩選條件
- 60天內看過信貸(卡友貸)網頁
- 60天內信貸試算有結果但未送件
- 60天內申請信貸(卡友貸)未送件
- 60天內進到信貸試算第1頁未送件
- 45天內看過理財相關網頁
- ...

### 衡量標準
- 業務：名單轉換率
- Baseline模型：若以分類問題來建模，建議使用AUC
- Deep Learning模型：其他合適的衡量方法

### 現有模型成效
- 無(僅有2018年的舊模型相關檔案)

### 資料來源(data resource)
- 透過Google Cloud Platform(GCP)Storage提供
- 建模時間區間：2019年11月1日-2020年4月30日
- 母體：[ClientID, or 瀏覽器ID](https://www.owox.com/blog/use-cases/google-analytics-client-id/)
- x值：欄位解釋：[Table schema](https://support.google.com/analytics/answer/3437719?hl=en)
- y值：點選至信貸(卡友貸)相對應頁面
    - 信貸：/s/PersonalLoanApply/Attachment/Upload
    - 卡友貸：/EsunCreditweb/txnservice/mlapsend


### 會議規劃(meeting schedule)
- 建議初期每兩週一次例會，開始建模後視情況調整為每三到四週一次例會

### 討論(discussion)
- 樣本蒐集定義? 是進入玉山官網還是特定頁面?
    - 樣本為每天造訪玉山官網的顧客的Log紀錄，載具包含手機、電腦、平板，留存的格式都一樣，為不同的瀏覽器會有不同的clientID。 
- Y值定義? 觸發行為後多久進到申請頁面?
    - Y值定義:
        - 信貸線上申請：  /s/PersonalLoanApply/Attachment/Upload
        - 卡友貸線上申請：  /EsunCreditweb/txnservice/mlapsend
    - 觸發行為定義:
        - 現行的rule-based方法，是在GA或是Facebook後台設定條件，如果瀏覽過預先定義的頁面就會進入名單30天(或是可設定的天數)
- 資料細節(待實作時更新)：
    - Y值0和1的比例?
    - Training和Testing Data怎麼切?
- 模型實作：
    - 玉山負責feature engineering和使用tree-based model(LightGBM)作為baseline
    - 中研院負責Deep Learning Based Model，倚任副理建議可加入sequential或graph embedding


### 待辦(to-do)
- 保密協議
- 本周(5/8前)將資料交付給中研院
    - 資料說明:
        - 範例樣本為2020/1/1，一小群顧客的資料樣貌
        - 2020年4月間(2020/4/1-4/30)顧客曾經造訪特定頁面即為y=1(y值定義如下)
        - clientId(y=0): 2020年4月間(2020/4/1-4/30)，<span style="color:blue">**未曾造訪**</span>特定頁面的顧客Id
        - 由於clientID是瀏覽器ID(clientId)，二月的clientId在一月時可能還不存在;或是一月存在的clientId，二月已經被清除了
            - clientId(y=1): 2020年4月間(2020/4/1-4/30)，曾經造訪特定頁面的顧客Id
            - 登入log資訊即為含有特徵以及標籤值(pagePath)的顧客造訪log軌跡
        - 登入Log資訊 2020/01 (y=0)：代表四月中未曾造訪特定頁面的顧客，在1月間的log瀏覽足跡
        - 特徵解釋請參考官方說明([BigQuery Export schema](https://support.google.com/analytics/answer/3437719?hl=en))
            - 舉例：提供資料中的pageviews欄位即為BigQuery中的totals.pageviews	

    - y值定義(pagePath):
        - 信貸線上申請：  /s/PersonalLoanApply/Attachment/Upload
        - 卡友貸線上申請：  /EsunCreditweb/txnservice/mlapsend
    - 建模資料
        - [範例樣本(一天) 277 KB](https://storage.cloud.google.com/cft_shared/v01_demo_features_y_in_one_day)
        - [clientId(y=0 in 2020/04) 120,000筆, 2.46 MB](https://storage.cloud.google.com/cft_shared/v01_id_random_y0_202004)
        - [clientId(y=1 in 2020/04) 11,007筆, 230 KB](https://storage.cloud.google.com/cft_shared/v01_id_all_y1_202004)
        - [登入Log資訊 2020/01 (y=0 in 2020/04) 561 MB](https://storage.cloud.google.com/cft_shared/v01_selected_y0_features_y_range_2020_01)
        - [登入Log資訊 2020/02 (y=0 in 2020/04) 686 MB](https://storage.cloud.google.com/cft_shared/v01_selected_y0_features_y_range_2020_02)
        - [登入Log資訊 2020/03 (y=0 in 2020/04) 933 MB](https://storage.cloud.google.com/cft_shared/v01_selected_y0_features_y_range_2020_03)
        - [登入Log資訊 2020/04 (y=0 in 2020/04) 1.2 GB](https://storage.cloud.google.com/cft_shared/v01_selected_y0_features_y_range_2020_04)
        - [登入Log資訊 2020/01-04 (y=1 in 2020/04) 761 MB](https://storage.cloud.google.com/cft_shared/v01_y1_features_y_range_2020_01to04)

## Collaboration
- [Dr. Chuan-Ju Wang ](https://www.citi.sinica.edu.tw/pages/cjwang/index_zh.html)
- [Research Labs](https://cfda.csie.org/)

--- 
## Archive
### Data related
- Q1: Data size and seasonality
    - Size: For raw data for one day, 1.33GB, 275,417 rows 
    - Seasonality: N/A
- Q2: Check compliance and regulation
    - It should be okay since there is no personal info in GA data set
- Q3: Deliver result
    1. identify critical feature 
    2. workflow in GA

### Project related
1. 定期: 同步提供
1. 目標商品: 信貸以及卡友貸
1. 行銷名單: 瀏覽器ID(customDimention)
1. 衡量標準: AUC分類問題(classification, 0/1)
1. 追蹤成效: 後續與業務發展部越虹討論(過去為dashboard)
1. 資料來源: 透過GCP提供中研院王老師資料

### Question set
- Q1 產品類型？
    - 特徵X
        - 目前條件皆為人工定義，請問資料來源只有GA資料嗎？
            - YES, 不需外接資料
    - 標籤Y
        - 貸款相關：除了信貸、卡友貸還有其他貸款商品嗎？
            - 此專案範疇以信貸及卡友貸為優先考慮項目　
    - 欄位分類
        * visitorId
        * visitNumber
        * visitId
        * visitStartTime
        * date
        * totals
        * trafficSource
        * device
        * geoNetwork
        * customDimensions
        * hits
        * fullVisitorId
        * userId
        * clientId
        * channelGrouping
        * socialEngagementType

- Q2 資料來源？
    - 這些資訊是否已經留存於BigQuery內
        - YES
- Q3 問題延伸
    - 串接外部資料可行性