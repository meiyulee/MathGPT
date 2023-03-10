# 分析方法說明文件

## 介紹

傳統迴歸分析方法已經行之多年並成為尋找變量關聯性的分析方法主流。且不提傳統迴歸分析方法的三個基本假設，目前最大的應用問題發生在數字。原本傳統迴歸分析法是用於閉集合(close set)的「累加性數字」分析法，而我們目前遇到的數字則很多都是正在發展中的數字集(number set)。此點已經讓方法發生的應用性錯誤。因此，我們需要重新思考如何建立變量關聯性的分析方法。

很幸運地，我們挖掘出迴歸分析法的本質：選擇自變數的目的是能夠達到愈高解釋力愈好。而這點也出現在計量經濟學課本中。因此，想要解決成對樣本的數學關係，就是擬合出一條數學方程式。統計學的迴歸分析認為此數學方程式為直線模式(linear model)，所以我們所見的範例都具有良好的直線關係。然而，這世界的真實數字未必有那麼美好的直線關係，如此就會產生布精準的估計方程式。若研究人員只在意必須符合直線模式，將數字轉換來轉換去，最終這些研究可能已經偏題。

在大數據和人工智能時代下，數據驅動產生模型是必然的一條路。而 **建立精準的成對樣本估計方程式** 是我們的關鍵目的。對此，我們得先了解迴歸分析法的要素有哪些。

- 自變數選擇
- 應變數選擇
- 樣本數選擇
- 期望值模型形式
- 殘差
  - 殘差的機率分布
  - 殘差建立變異數異質性模型
  - 殘差建立AR(1)誤差模型
  - 殘差建立變異數異質性模型後，剩餘殘差再建立AR(1)誤差模型

在這，我列出了迴歸分析法內的要素。這不是從假設檢定的角度出發，而是採用 **數學建模** 角度思考迴歸分析法。為了解說「多線段法(lines combined method)」，我點出關鍵的要素有：

- 自變數選擇
- 樣本數選擇
- 期望值模型形式

在釋出軟體的第一版內容中已經提到「數字種類」，此處不再贅述。第二點的樣本數選擇和第三點期望值模型形式成為改良迴歸分析法成為「多線段法」的關鍵原因。

## 要能達到精準的數學模型 - 多線段法

首先要從第三點開始說明。迴歸分析法本身就是希望為成對樣本建構配適良好的數學模型，只是其理論假設為直線模式。一旦遇到成對樣本存在背離直線模式的關係，此假設就需被拋棄。而放寬此假設並沒有任何負擔，也沒有過度配適(overfitting)的問題。一切都是為了建立數字的精準模型為目的。在此前提下，期望值模型形式可以有海量般的數學函數。在一個或超過一個自變數下，我們追求模型的判定係數極大，這也代表同時達到MSE極小原則。

在發展中的成對樣本中，一段時間後就會增加新的數字。這表示樣本數多寡成為影響因素。若要為成對樣本建立精準的數學模型，那我們就得由數字自己找出多少樣本數就足夠達到最精準的結果。如此一來，改變了使用傳統迴歸分析時，我們自己決定想要放多少樣本數，轉為由每增加一個數字就得跑一次迴歸。跑完迴歸就記錄下判定係數，做到我們追求模型判定係數極大原則。

於是，多線段法由此而生！

在成對樣本順序下，我們可以逐一加入成對樣本跑迴歸。判定的參數有

- 判定係數 (The difference R2)
> 預設 The difference R2 = 0 代表只要判定係數下降就開始新的估計線

- 每次跑迴歸所需的最少樣本數 (the minimum data number of each line)
> 如果最少樣本數 = 全體數據量，多線段法下的直線模式如傳統迴歸分析結果。

## 多線段法運用在期望值模型上有三種形式

多線段法是分析方法的原理，而期望值模型的數學形式則可以是

- 直線模式 (linear model)
- 非直線模式 (nonlinear model)
- 曲線化線性模式 (Curvilinear model, curve linear model)


## 運算機制

選擇最佳的估計方程式須滿足

1. 估計方程式個數少 (在數據集內可產生的迴歸線個數)
2. 數學函數要簡單最好是線性
3. <b><font color="red">MSE 越小越好</font></b>

以第3點為最重要。在可接受的 MSE 之下以簡單的數學函數為準，最後才考慮使用最少的估計方程式個數。原因在於MSE愈小代表「估計方程式組合」更具有精準度。數學函數簡單化可以在少量的樣本
數下建立連續的數學規律。最少的估計方程式個數可使計算容易且程式簡單化。

### 1.直線模式

- 適用以線段或多線段能夠建立估計模式的數據
- 當使用傳統迴歸分析後，解釋能力較差且資料規律不是線性狀況下，補救措施為降低 the minimum data number of each line 的設定數字，也就是每段迴歸線以最少的數據量去跑，直到新增加的數字導致判定係數下降
- 增加更多條迴歸線去調整和適應數據的非直線規律
- 適合少量的樣本總數就能建立連續型的數學規律
- 估計方程式在計算時非常簡單且程式也是簡單化

### 2.非直線模式

- 適用於其數據庫的數學函數或多個數學函數的數據集(data set)
- 其解釋能力較高並在數字規律不是線性狀況時可使用
- 此法的預測能力較差，不如線性模式的強度
- 樣本數須達 1,000 筆以上才能建立連續的數學規律
- 估計方程式計算時較不容易且程式是較為複雜形式

### 3.曲線化直線模式

- 適用於大部分複雜數學組成的數學函數的資料,其解釋能力十分較高在資料規律
不是線性狀況
- 不能做預測只能建立資料的數學模式
- 樣本數須達 10,000 筆以上才能建立連續的數學規律
- 估計方程式計算時十分不容易且程式是十分困難

## 變異數異質性模型 (heteroskedastic model)

使用本軟體運算變異數異質性模型，須先完成「期望值模型」運算後，得到殘差。殘差數據儲存在「residual_plot.txt」。
將殘差導入Excel，做為Y值。以期望值模型的自變數為X。
根據軟體可導入的數據格式(X, Y)，相當於A欄為X數字，B欄為Y數字，在Excel排好後，複製貼到新的txt檔。

變異數異質性模型設計如下：

$$
|residual|= G(X) + residual^{*} 
$$

設定新的殘差為

$$
residual^{**} = \frac{residual}{the estimated |residual|} \\
$$

$i = 1, 2, ..., n$。

## AR(1) 誤差模型

模型設計如下：

$\varepsilon_{t}=K(\varepsilon_{t-1})+u_{t}$

其中， $t = 2, 3, ...,n=$ 樣本順序。 $K(\bullet)$ 可為直線模式、非直線模式、曲線化直線模式。但我們其實無法得到誤差值，只能得到殘差值。所以模型改為

$e_{t}=K(e_{t-1})+u_{t}$

---

1. 有關多線段法建模方法和應用，請參考

  - Wang, K.W., Wang, K.S., Lee, M.Y., 2023, *Accurate New Stock Analytic Model: Ability over moving average*, sold at the [Amazon ebook store](https://www.amazon.com/dp/B0BS2XS8NM/).
  - Lee, M.Y., 2022, Line-combined Method and Trend Dynamics, manuscript on ResearchGate. https://doi.org/10.13140/RG.2.2.22765.05603
  - Lee, M.Y., 2022, 道瓊工業指數急速拉升的建模方法可行性, manuscript on ResearchGate. https://doi.org/10.13140/RG.2.2.26233.54885/1
  - Lee, M.Y., 2022, Analyze Alphabet Closes from 7/1/2021~9/30/2022, using Regression model, manuscript on ResearchGate. https://doi.org/10.13140/RG.2.2.28645.27363


2. 有關變異數異質性模型

  - Chih-Wen Hsiao, Ya-Chuan Chan*, Mei-Yu Lee, Hsi-Peng Lu, 2021, Heteroscedasticity and Precise Estimation Model Approach for Complex Financial Time-Series Data: An Example of Taiwan Stock Index Futures before and during COVID-19, Mathematics, 9(21), 2719.

  - 王冠先、李玫郁，「統計學不能做為大數據分析的工具-原因與補正」，機統股份有限公司出版，2019年。[博客來網路書店](https://www.books.com.tw/products/0010844752)

3. AR(1)誤差模型如何在精準建模中使用，請參考

  - 王冠先、李玫郁，「統計學不能做為大數據分析的工具-原因與補正」，機統股份有限公司出版，2019年。[博客來網路書店](https://www.books.com.tw/products/0010844752)
  - Lee, M.Y., 2022, *Demythologize Durbin-Watson Test Statistic: From the analysis of the sampling distribution, critical values and affected factors*, sold at the [Amazon ebook store](https://www.amazon.com/dp/B09QT7YF1S/)