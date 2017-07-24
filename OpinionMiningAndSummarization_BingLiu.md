# Opinion Mining & Summarization - sentiment analysis

---

## introduction - facts and opinion

<br>

### two main types of textual information.

### Fact 事實
### Opinion 意見

most current information processing techique (Ex. search engine) work with facts.

**Facts can be expressed with topic keywords.**

> 事實可以用主題關鍵字表達, Ex 搜尋引擎

<br>

### search engine do not search for opinions

- opinion are hard to express with a few keywords.
  ex. How do people think of Motorola Cell phones?

- Current search ranking strategy is not appropriate for opinion retrieval/search.

> 意見很難被少量的 keywords 找到
> 目前的搜尋引擎排名不適合拿來做意見搜索

---

## Introduction – user generated content

<br>

### Word-of-mouth on the web

- One can express personal experiences and opinions on almost anything, at review sites, forums, discussion groups, blogs...(call the user generated content)

- They contain valuable information.

- Web/global scale: No longer - one;s circle of friends

> 一個可以發表任何事情, 經驗, 意見的地方 -> user generated content
> 包含有價值的資訊
> 全球的規模而不是朋友的圈子

<br>

### Our interest: to mine opinions expressed in the user generated content

- An intellectually very challenging problem.
- practically very useful.

> 挖掘 user generated content 中 的 opinions

---

## Introduction - Applications

- Businesses and organizations
- individuals
- ads placements
- Opinion retrieval/search

> Application:  Businesses and organizations, individuals, ads placements, Opinion retrieval/search

---

## Opinion search

(Liu, Web Data Mining book, 2007)

- Can you search for opinion as conveniently as general Web search?

- Whenever you need to make a decision, you may want some opinion from others,
    - wouldn't it be nice?
        you can find them on a search system instantly, by issuing queries such as
        - Opinions: `Motorola cell phones`
        - comparisons: `Motorola vs Nokia`

**Can't not be done yet! Very hard!**

> Opinion search 現在並不能像一般搜索一樣
> 搜尋 時常會出現 `詢問意見` or `比較`, 
但是現階段 opinion search 並無法 完全做好

---

## Typical opinion search queries

- Find the opinion of a person or organization(`opinion holder`) on a particular object or a feature of the object.

    > 找尋 opinion-holder 在特定對象 or 特徵對像 中的意見

- Find positive and/or negative opinions on a particular object(or some features of the object)
 
    > 找尋正面 or 負面的意見 在 特定對象 或者 特徵對象

- Find how opinions on an object change over time.
    
    > 找尋意見隨著時間的變化

- How object A compares with objects B
    - Gmail vs Hotmail
    
    > 找尋 object 之間的關聯

---

## Find the opinion of a person on X

- In some cases, the general search engine can handle it, i.e using suitable keywords.
    - Bill Clinton's opinion on abortion.
    > 某些案例裡, 使用適當的關鍵字可以找到 某人的意見 對於 X

- Reason
    - One person or organization usually has only one opinion on a  topic.
    - The opion is likely contained in single document.
    - Thus, a good keyword query may be sufficient.
    
    > 理由是
    >
    > * 一個人或組織通常對於特定 topic 只有一項意見
    >
    > * 意見通常會被包含在一篇文章內

---

## Find opinions on a object

**We use product reviews as an example :**

- Searching for opinion in product reviews is different from general Web search.
    - E.g search for opinion on "Motorola RAZR V3"

- General Web search (for a fact): rank pages according to some authority and relevance scores.
    - the user views the first page(if the search is perfect).
    - **One fact = multiple facts.**
    > 對於 General web search 來說, 一項事實其實是多個事實的集合
- Opinion search: rank is desirable, however
    - reading only the review ranked at the top is not appropriate because it is only the opinion of one person.
    - **One opinion != Multiple opinion**
    > 對於 opinion search 來說, 排名並無太大意義因為第一名也只是一個人的意見.

---

## Search opinion(contd)

**Ranking**

- produce two rankings
    - Positive opinions and Negative opinions
    - some kind of summary of both, e.g # of each
    > 兩種排名, positive and negative, 算是兩種的一個總結

- Or, one ranking but
    - The top (say 30) reviews should reflect the natural disbution of all reviews (assume that there is no spam), i.e, with the right balance of positive and negative reviews.
    > 或者 一種排名 但是需要均勻的分佈在正面與負面中.

**Questions**

- Should the user reads all the top reviews? OR
- Should the sysem prepare a summary of the reviews?

    > 問題是 使用者需要 看過所有排名前面的 評論嗎?
    >
    > 或者系統應該提供 評論的 總結?
  
<br>

--- 
---

<br>

# Opinion mining - the abstraction
(Hu and Liu, KDD-04; Liu, Web Data Mining book 2007)

- Basic components of an opinion
 - opinion holder: the person of organization that holds a specific opinion on a particular 
 - Object: on which an opinion is expressed
 - opinion: a view, attitude, or appraisal on an object from an opinion holder.
 > Opinion 是由  opinion-holder, object, opinion所組成的
 
- Objectives of opinion mining: many...
 > opinion mining 的目標 : a lot

- Let us abstract the problem
    - put existing research into a common framework
- We use consumer reviews of products to develop the ideas. Other opinionated contexts are similaar.
 > 使用 消費者評論 來實現 idea

---

## Object/entity

- Definition(object): An object `O` is an entity which can be a product, person, event, organization, or topic `O` is represented as
    
    - a hierarchy of components, subcomponents and so on..
    
    - each node represents a component and is associated with a set of attributes of the component..
    
    - `O` is the root node(which also has a set of attributes)
    
    > 定義 `O` 是一個實體, 可以是一個人, 一個產品, 一個組織 或者
    > 一個有階級的組件 or 部件
    > 每個 node 表示一個組件, 並且與組件的一組屬性相關聯
    > `O` 表示 主節點, 同樣有著一組屬性

- An opinion can be expressed on any node or attribute of the node.
 > opinion 可以被任何node or attribute 表達出來

- to simplify our discussion, we use `features` to represent both components and attributes.
    - The term `feature` should be understood in a **Broad sense**
        product feature, topic or sub-topic, event or sub-event, etc

> 為了簡化討論我們使用 廣義的 `features` 來表達 components and attributes.
> `O` 本身也是個 `feature`

---

## Opinion mining tasks(contd)

**At the feature level**

- Task 1 : Identifying and extracting object features that have been commented on in each review.
- Task 2 : Determining whether the opinions on the features are postive, negative or nrutral.
- Task 3 : Grouping synonyms of features

produce a feature-based opinion summary of multiple reviews.

> 在 Feature-Level
> 有三個主要任務
> > * 識別和提取已註釋的 object feature.
> > * 判斷feature is positive, negative or neutral
> > * 把同義詞 feature  grouping 起來
>
> 最後基於多個評論產生 feature-based opinion

**Opinion holder**

identify holders is also useful. e.g in news article, ,etc, but they are usually known in the user generated content, i.e , auther of the posts.

> 識別 opinion-holder  同樣有幫助, 例如報導的作者, 但是他們通常是已知的


---

## More at the feature level

`F` : the set of features
`W` : the synonyms of each feature

> `F`表示 一組feature
> `W`表示 每個feature 的同義詞

- problem 1 :
    Both `F` and `W` are unknown.
    We need to perform all three tasks.
- problem 2 : 
    F is known but w is unknown.
    - All three tasks are still needed. Task 3 is easier.
    - It becomes the problem of matching the discovered featured with the set of given features F.
   
- problem 3 : 
    Both `W` and `F` is known.
    - Only task 2 is needed.

>  問題是
> * 如果`F`, `W` 皆未知, 需要執行所有tasks.
> * 如果`W` 未知, Tasks 3 的問題會變成是 匹配 新發現的 feature 與 已給定 feature 的 feature 
> * 如果`W`, `F` 皆已知, 只需要執行 task 2

<br>

---

<br>


# Document-Level sentiment classification

---

## Sentiment clssifiction

**Classify document based on the overall sentiments expressed by opinion holders(authrs),**

> Classify document 是基於 瀏覽全部 opinion-holder 所表達的情緒.

- Postive, negative and (possibly) neutral.
- Since in our model an object O itself is also a feature, then sentiment classification essentially determines the opinion expressed on O in each document

> 由於 `O` 本身是個 feature, 情緒分類等於是 所有文件中 對於 `O` 所表達的意見

**Similar but different from topic-based text classification**

- In topic-based text classification, topic word are important.
- In sentiment classification, sentiment word are more important e.g excellent, horrible, bad, worst etc.

> 跟主題式的分類器相比有點相似但不同
>
> 在主題式分類器中, 主題字是重要的
> 
> 但在情緒分類器中, 情緒字眼更重要 例如  execllent, horrible

---

## Unsupervised review classification
(Turney, ACL-02)

無監督評論分類器

**Data**

- review from epinions.com on automobiles, banks, movies, and travel destinations.

> 資料來自銀行, 旅遊, 電影之類的評論

**Approach**

- Step 1 
	- part-of-speech tagging
	- Extracting two consecutive words(two-word phrsed) from reviews if their tags conform to some given patterens, e.g
	
	> 第一步驟 
	>
	> 詞性標籤
	>	
	> 提取兩個連續詞, 如果他們的標籤符合某種給訂的模式

- Step 2 Estimate the semantic orientation (SO) of the extracted phrases

	- Use the `PMI (point mutual information)`

	- Semantic orientation (SO)

	- Using AltaVista(search engine) near operator to do serch to find the number of hits to compute `PMI` and `SO`
	
	> 估計提取出來的 短語的 `SO` 值
	> 使用 search engine 去找到  鄰近 詞 的數量 來計算  `PMI` and `SO`
	
- Step 3 Compute the average SO of all phrases

	- classify the review as recommend if average SO is positive, not recommended otherwise.
	
	> 計算所有短語的 平均 SO 值
	>
	> 如果 SO 值  positive 則表示推薦
	
---

## Sentiment classificatino using machine learning methods
(Pang et al, EMNLP-02)

- This paper directly applied several machine learning techniques to classify movie reviews into positive and negative.
- Threee classificatino techniques were trie:
	- Naive Bayes
	- Max entropy
	- Support vector machine
- Pre-processing settings: negation tag, unigram(single words), bigram, POS tag, position.
- SVM: the best accuracy 83%.

> 這份paper 使用了三種 machine lerning 來實作電影分類器 (正面與負面)
> Naive Bayes, Max entropy and SVM
> 預處理使用了包含 negation tag, unigram(single words), bigram, POS tag, position 等等方式
> 最佳解是 SVM + unigram

---

## Review classification by scoring fratures

(Dave, Lawrence and Pennock, WWW-03)

---

## Other related works

- Using PMI, syntactic relations and other attributes with SVM (Mullen and Collier, EMNLP-04).

- Sentiment classification considering rating scales (Pang and Lee, ACL-05).
  
- Comparing supervised and unsupervised methods (Chaovalit and Zhou, HICSS-05)

- Using semi-supervised learning (Goldberg and Zhu, Workshop on TextGraphs, at HLT-NAAL-06).
- Review identification and sentiment classification of reviews (Ng, Dasgupta and Arifin, ACL-06).
 
- Sentiment classification on customer feedback data (Gamon, Coling-04).
  
- Comparative experiments (Cui et al. AAAI-06)
- Many more ...

<br>
  
--- 
---

<br>
 

# Sentence-Level sentiment analysis
 
 - Document-level sentiment classification is too coarse for most applications.
 - Let us move to the sentence level.
 - Much of the work on sentence level sentiment analysis focuses on identifying `subjective sentiences` in new articles.
 	- Classification : objective and subjective.
 	- All techniques use some forms of machine learning
 	- E.g., using a naïve Bayesian classifier with a set of data features/attributes extracted from training sentences (Wiebe et al. ACL-99).

> **對大多數的 application 來說, document-level 太過於粗糙**
> 大多數的 sentiment-level 在 主要是在確定文章中主觀的句子
> 分類器 : 主觀與非主觀
> 都使用了某種程度的機器學習

---

## Using learnt patterns 

(Rilloff and Wiebe, EMNLP-03)

---

##  Subjectivity and polarity (orientation)

(Yu and Hazivassiloglou, EMNLP-03)

---

##  Other related work

- Consider gradable adjectives (Hatzivassiloglou and Wiebe, Coling- 00)
  
- Semi-supervised learning with the initial training set identified by some strong patterns and then applying NB or self-training (Wiebe and Riloff, CICLing-05).

- Finding strength of opinions at the clause level (Wilson et al. AAAI- 04).
  
- Sum up orientations of opinion words in a sentence (or within some word window) (Kim and Hovy, COLING-04).

- Find clause or phrase polarities based on priori opinion words and classification (Wilson et al. EMNLP-05)

- Semi-supervised learning to classify sentences in reviews (Gamon et al. IDA-05).
  
- Sentiment sentence retrieval (Eguchi and Lavrendo, EMNLP-06)

---

## Let us go further?

- Sentiment classification at both document and sentence(or clause ) levels are useful, but 
	- They don't find what the opinion holder liked and disliked.

- An negative sentiment on an object
	- does not mean that the opinion holder dislike everything about the object.

- An positive sentiment on an object
	- doed not mean that the opinion holder likes everything about the object.

**We need to gl to the feature level**

> Sentiment classification and document level 找不到 opinion-holder 喜歡與不喜歡什麼
> 一個 負面的 object 並不代表 opinion-holder 討厭 object的所有事情, 反之亦然.

---

## But before we go further 

- Let us discuss `Opinion words` and `Phrases` (also called polar words, opinion bearing words, etc.)

 - Postive: beautiful, worderful, good, amazing
 - Negative: bad, poor, terrible, cost someone an arm and a leg.

- They are instrimental for opinion mining(obviously)
- Three main ways to compile such a list
	- Manual approach: not a bad idea, only an one-time effort.
	- Corpus-based approached
	- Dictionary-based approaches

> 定義opinion words
> > 具有煽動性
> 
> 有三種產生方式
> > * 手動產生
> > * 語料庫
> > * 辭典
 
- **important to note**
	- some opinion words are context indepentent
	- Some are context dependent

	> 一些 opinion word  是上下文獨立的, 有些則是相關的
	
---

## Corpus-based approaches

- Rely on syntactic or co-occirrence patterns in large corpora (Hazivassiloglou and McKeown, ACL-97; Turney, ACL- 02; Yu and Hazivassiloglou, EMNLP-03; Kanayama and Nasukawa, EMNLP-06; Ding and Liu SIGIR-07)

    - Can find domain (not context!) dependent orientations (positive, negative, or neutral).

- (Turney, ACL-02) and (Yu and Hazivassiloglou,
EMNLP-03) are similar.

    - Assign opinion orientations (polarities) to words/phrases.

    - (Yu and Hazivassiloglou, EMNLP-03) is different from (Turney, ACL-02)
 
 	    - use more seed words (rather than two) and use log- likelihood ratio (rather than PMI).  

---

## Corpus-based approaches(contd)

- Use constraints (or conventions) on connectives to identify opinion words (Hazivassiloglou and McKeown, ACL-97; Kanayama and Nasukawa, EMNLP-06; Ding and Liu, 2007). E.g.,

> 在連接詞上使用約束來識別意見詞

- Conjunction: conjoined adjectives usually have the same orientation (Hazivassiloglou and McKeown, ACL-97).
	
	- E.g., “This car is beautiful and spacious.” (conjunction)
	- learning using:
		- log-linear model: determine if two conjoined adjective are of the same or different orientations.
		- Clustering : produce two sets of words: postive and negative
	- Corpus: 21million word 1987 Wall Street Journal corpus.

> 連接 連接形容詞通常具有相同的方向
> 使用 log-linear model, 判斷連接詞兩邊的詞是否同個方向
> 類聚 positive and negative 兩種類型的詞

---

## Corpus-based approaches(contd)

- (Kanayama and Nasukawa, EMNLP-06) takes a similar approach to (Hazivassiloglou and McKeown, ACL-97) but for Japanese words:
	
	- instead of using learning, it uses two criteria to determine whether to add a word to positive or negative lexicon.
	- Have an initial seed lexicon of positive and negative words.

> 沒有學習直接使用兩種標準判斷應該加入positive or negative 詞庫
> 有基礎的種子辭庫

---

## Corpus-based approaches(contd)


- Ding and Liu, 2007) also exploits constraints on connectives, but with two differences

	- It uses them to assign opinion orientations to product features (more on this later).
		- One word may indicate different opinions in the same domain.
			-   “The battery life is long” (+) and “It takes a long time to focus” (-).
		
		- Find domain opinion words is insufficient.

	- It can be used without a large corpus.

> 也對連接詞使用了限制, 但是有兩個不同
> > * 相同的詞在不同領域可能有不同含義
> > * 找尋 領域  opinion 是不足的
> 
> 在 corpus 不夠大時也可以使用

---

## Dictionary-based approaches

- Typically use WordNet’s synsets and hierarchies to
acquire opinion words
 - Start with a small seed set of opinion words.
 - Use the set to search for synonyms and antonyms in WordNet (Hu and Liu, KDD-04; Kim and Hovy, COLING-04).
 - Manual inspection may be used afterward.

- Use additional information (e.g., glosses) from WordNet (Andreevskaia and Bergler, EACL-06) and learning (Esuti and Sebastiani, CIKM-05).


- Weakness of the approach: Do not find context dependent opinion words, e.g., small, long, fast.

> 從一個種子意見詞開始, 搜索同義詞和反義詞
> 之後可以手動檢查
> 弱點是找不到上下文的意見詞

<br>

---
---

<br>

# Feature-based opinion mining and summarization

- Again focus on reviews (easier to work in a concrete domain!)

- Objective: find what reviewers (opinion holders) liked and disliked

	- Product features and opinions on the features

- Since the number of reviews on an object can be large, an opinion summary should be produced.

	- Desirable to be a structured summary.
	- Easy to visualize and to compare.
	- Analogous to but different from multi-document summarization.

---

## The tasks

 - Recall the three tasks in our model.
 	- Task 1: Extract object features that have been commented on in each review.
	- Task 2: Determine whether the opinions on the features are positive, negative or neutral.
	- Task 3: Group feature synonyms.   Produce a summary
 
 - Task 2 may not be needed depending on the format of reviews.

--- 

## Different review format

- Format 1 - Pros, Cons and detailed review: The reviewer is asked to describe Pros and Cons separately and also write a detailed review. Epinions.com uses this format.

> 分別描述利弊, 詳細

-  Format 2 - Pros and Cons: The reviewer is asked to describe Pros and Cons separately. Cnet.com used to use this format.

> 分別描述利弊

- Format 3 - free format: The reviewer can write freely, i.e., no separation of Pros and Cons. Amazon.com uses this format.

> 免費格式, 自由輸入

---

##  Feature-based opinion summary (Hu and Liu, KDD-04)

> 在句子中找到 關鍵字, 並判斷 該句的正負面傾向, 然後做統計後 當作 feature

---

##  Feature extraction from Pros and Cons of Format 1 (Liu et al WWW-03; Hu and Liu, AAAI-CAAW-05)

- Observation: Each sentence segment in Pros or Cons contains only one feature. Sentence segments can be separated by commas, periods, semi-colons, hyphens, ‘&’’s, ‘and’’s, ‘but’’s, etc.

> 每段  sentence 句 中只有一個 feature

---

##  Extraction  using label sequential rules

- Label sequential rules (LSR) are a special kind of sequential patterns, discovered from sequences.
- LSR Mining is supervised (Liu’s Web mining book 2006).
- The training data set is a set of sequences, e.g.,

	`Included memory is stingy`
	
	is turned into a sequence with POS tags.
	
	<{included, VB}{memory, NN}{is, VB}{stingy, JJ}>
	
	then turned into
	
	<{included, VB}{`$feature`, NN}{is, VB}{stingy, JJ}>

> LSR 是種順序模式的特殊類型, 從序列中發現
> 屬於監督學習
> 範例如上

---

## Using LSRs for extraction

- Based on a set of training sequences, we can mine label sequential rules, e.g.,

```
<{easy, JJ }{to}{*, VB}> 變成

<{easy, JJ}{to}{$feature, VB}>

[sup = 10%, conf = 95%]

```


- Feature Extraction

	- Only the right hand side of each rule is needed.
	- The word in the sentence segment of a new review that matches $feature is extracted.
	- We need to deal with conflict resolution also
(multiple rules are applicable).

> 提取符合 $feature 規則的單詞


---

## Extraction of features of format2 and 3

- Reviews of these formats are usually complete sentences 

> 評論通常來自完整的句子
	
- the pictures are very clear.

    - Explicit feature: picture
	> 明確的 feature

- “It is small enough to fit easily in a coat pocket or purse.”

	- Implicit feature: size
	
	> 隱含的 feature

- Extraction: Frequency based approach
	- Frequent features
  	- Infrequent features

    > 基於頻率的提取
    
---

## Frequency based approach

(Hu and Liu, KDD-04; Liu, Web Data Mining book 2007)



- Frequent features: those features that have been talked about by many reviewers.
 
- Use sequential pattern mining
  
- Why the frequency based approach
	- Different reviewers tell different stories (irrelevant)
  - When product features are discussed, the words that they use converge.
  - They are main features.
  
- Sequential pattern mining finds`frequent phrases`.
  
- Froogle has an implementation of the approach (no POS restriction).

> 被許多評論使用的 feature
> 使用順序模式挖掘
> 為何使用頻率方式？
> > * 不同的評論講述不同的故事
> > * 當討論 feature 時, 使用的詞會匯集在一起
> > * 而他們是主要特徵
>
> 挖掘頻繁使用的短語

---

## Using part-of relationship and the Web (Popescu and Etzioni, EMNLP-05)

- Improved (Hu and Liu, KDD-04) by removing those frequent noun phrases that may not be features: better precision (a small drop in recall).

- It identifies part-of relationship
	- Each noun phrase is given a pointwise mutual information score between the phrase and part discriminators associated with the product class, e.g., a scanner class.
	
	- The part discriminators for the scanner class are, “of scanner”, “scanner has”, “scanner comes with”, etc, which are used to find components or parts of scanners by searching on the Web: the KnowItAll approach, (Etzioni et al, WWW-04).

> 移除那些無用的feature, 以達到更好的精度

---

##  Infrequent features extraction

- How to find the infrequent features?
- Observation: the same opinion word can be used to describe different features and objects.

  - “The pictures are absolutely amazing.”
  - “The software that comes with it is amazing.”

```
Frequent features -> Opinion words -> Infrequent features
```

> 如何找到不常見的 features
> 
> 相同的 opinion word 可以被拿來描述不同的 features and objects


---

## Identify feature synonyms

- Liu et al (WWW-05) made an attempt using only WordNet.
  
- Carenini et al (K-CAP-05) proposed a more sophisticated method based on several similarity metrics, but it requires a taxonomy of features to be given.

	- The system merges each discovered feature to a feature node in the taxonomy.
  
	- The similarity metrics are defined based on string similarity, synonyms and other distances measured using WordNet.
  
	- Experimental results based on digital camera and DVD reviews show promising results.
  
- Many ideas in information integration are applicable.

---

##  Aggregation of opinion words (Hu and Liu, KDD-04; Ding and Liu, 2008)

---

##  Context dependent opinions

- Popescu and Etzioni (EMNLP-05) used
	- constraints of connectives in (Hazivassiloglou and McKeown, ACL-97), and some additional constraints, e.g., morphological relationships, synonymy and antonymy, and

	- relaxation labeling to propagate opinion orientations to words and features.

- Ding et al (2008) used

	- constraints of connectives both at intra-sentence and inter-
sentence levels, and

	- additional constraints of, e.g., TOO, BUT, NEGATION, .... to directly assign opinions to (f, s) with good results (>
0.85 of F-score).

---

## Some other related work

- Morinaga et al. (KDD-02).
- Yi et al. (ICDM-03)
- Kobayashi et al. (AAAI-CAAW-05)
- Ku et al. (AAAI-CAAW-05)
- Carenini et al (EACL-06)
- Kim and Hovy (ACL-06a)
- Kim and Hovy (ACL-06b)
- Eguchi and Lavrendo (EMNLP-06)   Zhuang et al (CIKM-06)
- Mei et al (WWW-2007)
- Many more

<br>

---

---

<br>


## Extractino of comparatives (Jinal and Liu, SIGIR-06, AAAI-06; Liu’s Web Data Mining book)

- Recall: Two types of evaluation
	- Direct opinions : "This car is bad"
	- Comprisons: "car X is not as good as car Y"

- They use different language constructs

> 兩種類型, 直接與比較
> 使用不同的語言結構

- Direct expression of sentiment are goood. Compareison may be better.
	- Good or bad, compared to what?
- Comparative Sentence Mining
	- Identify comparative sentences, and
	- extract comparative relations from them

> 直接表達情緒的結果可能是好的, 比較可能會更好
> 
> Comparative Sentence Mining
> > 識別比較句子
> > 
> > 提取比較句子的關係

---

##  Linguistic Perspective

- Comparative sentence use morphemes like
	- more/most, -er/-est, less/least and as.
	- then and as are used to make a `standard` againest which an entity is compared

> 比較句所使用的語素
> `and`, `as` 被拿來當作標準來比較 實體

**Limitations**

- Limited cinverage
	- Ex "in market capital, intel is way ahead of Amd"
- Non-comparatives with comparative words
	- Ex "in the context of speed, faster means better."
- **For human consumptino; no computational methods**

> 限制有
> 
> * 不具有比較詞的比較
> 
> * 沒有計算方法

---

## Types of comparatives: Gradable

- Gradable
	- Non-Equal Gradable: Relations of the types greater or less then
		- Keywords like better, ahead, beats, etc
		- Ex: "option of camera A is better than that of camare B"
	- Equative: Relations of the type equal to
		- keywords and phrases like equal to, same as , both, all
		- Ex, "camera A and camera B both come in 7MP"
	- Superlative: Relations of the type greater or less than all others
		 - Keywords and phrases like best, most, better than all
		 - Ex: "camera A is the cheapest camera available in market"

> 比較方法 : 分級
> * 不相等的等級
> * 同等
> * 最高級

---

## Types of comparatives: non-gradable

- non-gradable: Sentences that compare features of two or more objects, but do not grade them. Sentences which imply:
	- Object A is similar to or different from Object B with regard to some features.
	- Object A has feature F1, Object B has feature F2 (F1 and F2 are usually substitutable)
	- Object A has feature F, but object B does not have.

> 比較方法 : 不分級
> 
> 比較多個對象的 feature,  但不對其進行分級
> 
> 句子有
> 
> * object A 與 object B 類似或者不同於某些feature
> * object A 有 feature f1, object B 有 feature f2 (f1, f2 通常可替換)
> * object A 有 feature F, 但 object B 沒有

---

## Comparative Relation : gradable

- Definition : A gradable comparative relation captures the essence of a gradable comparative sentence and is represented with the following:
	- relation Word : the keyword used to express a comparative relation in a sentence.
	- features: a set of features being compared.
	- entityS1 and entuitS1: Sets of entities being compared.
	- type: non-equal gradable, equative or superlative.

> 比較關係 : 可分級
> 
> 定義 : 一個 可分級比較關係 描述了一個可分級比較句的本質, 有下列本質
> 
> * 關係詞, 用於表達比較關係的關鍵詞
> * features, 一組被比較的features
> * entityS1 and entityS2, 被比較的實體集合
> * type, 不同, 相同 or 最高級的比較


---

## Example: Comparative relations

- Ex1 : "car X  has better controls than car Y"

	- relatinoWord = better, features = controls, entityS1 = car X, entityS2 = car Y, type = non-equal-gradable.

- Ex2 : "car X and car Y have equal mileage"	
	- relationWord = equal, feature = mileage, entityS1 = car X, entittyS2 = {car Y, car Z}, type = non-equal-gradable

- Ex3 : "car x is cheaper than both car Y and car Z"
	
	- relationWord = cheaper, features= null, entityS1 = car X, entityS2 = {car Y, car Z}, type =non-equal-gradable

- Ex4 : "company X produces a variety of cars, but still best cars come from company Y"
	- relationWord=best, features=cars, entityS1=company1, entityS2=null, type= superlative

---

## Tasks

Given a collectino of evaluative texts

Task 1 : identify comparative sntences.
Task 2 : Categorize different types of comparative sentences.
Taks 3 : Extract comparative relations from the sentence.

> * 識別比較性文本
> * 對不同類型的句子進行分類
> * 從句子中提取比較關係


---

## Identify comparative sentences(Jinal and Liu, SIGIR-06)

**Keyword strategy**

- An observation: It is easy to find a small set of keywords that covers almost all comparative sentences, i.e with  a very high recall and a reasonable precision.
- We have compiled a list of 83 keywords used in comparative sentences, which includes:

	- Word with POS tags of JJR, JJS, RBR, RBS
		- POS tags are used as keyword instead of individual words.
		- Exceptions: more, less, most and least
	- Other indicative word like beat, exceed, ahead, etc
	- Phrases like in the lead, on par with , etc.

> 確定比較句子
> 
> 關鍵詞策略
> 
> 使用了 83 個 關鍵詞表
> 
> * 包含具有 JJR, JJS, RBR, RBS 的 POS 標籤的字
> * POS 用作關鍵詞而不是單詞
> * 例外 : more, less, most, least
> 
> 其他指示性詞 beat, exceed, ahead
> 
> 短語 

---

## 2 step learning strategy


- Step 1 : Extract sentence which contain at least a keyword(recall = 98%, precisino=32% on our data set for gradables)

- Step 2 : Use the naive Bayes(NB) classifier to classifier sentences into two classes
	- comparative and non-comparative
	- attributes: class sequential rules(CSRs) generated from sentence in step 1, e.g <{1}{2}{7, 8}> -> classi [sup=2/5, conf=3/4]

> * Step 1 提取包含至少一個關鍵字的句子
> * Step 2 使用 `NB` classifier 將 句子分類為兩種, 比較與非比較, 屬性為步驟一生成的類順序規則 CSRs

<br>

- **1. Sequence data preparation**
	
	- Use words within radius r of a keyword to form a sequence(word are replaced with POS tgs)

- **2. CSR Generation**
	- Use different minimum supports for different keywords (multiple minimum supports)
	- 13 manual rules, which were hard to generate automatically.

- **3. Learning using a NB classifier**

	- Use CSRs and manual rules as attributes to build a final classifier.

> * 使用關鍵字半徑 r 內的單詞 形成 一個列序(使用POS tag 替換)
> * 產生CSR
> 
> > * 對不同關鍵字使用不同的最低支持
> > * 13 個手動規則, 很難自動生成
> 使用 `NB` 分類器, 使用CSR 和手動規則作為最後的 屬性

---

##Classify differnt types of comparatives

- Classify comparative sentences into three types: non-equal gradable, equative, and superlative
	- SVM learner gave the best result.
	- Attribute set is the set of keywords.
	- If the sentence has a particular keyword in the attribute set, the corresponding value is 1, and 0 otherwise.

> 將比較句分為三類
> 
> * SVM 獲得最佳解
> * 屬性集是一組關鍵字
> * 如果句子在屬性集中具有特定關鍵字, 則值為1, 沒有則為0

---

## Extraction of comparative relations(Jindal and Liu, AAAI-06; Liu’s Web mining book 2006)

Assumptions

- There is only one relation in a sentence
- Entities and features are nouns (include nouns, plural nouns and proper nouns) and pronouns.
	- Adjectival comparatives
	- Does not deal with adverbial comparatives

3 steps

- Sequence data generation
- Label sequential rule (LSR) generation
- Build a sequential cover/extractor from LSRs

> 假設
> > 一句話中只有一個關係
> > 
> > entities and features 都是名詞
> > > 形容詞比較
> > > 
> > > 不比較副詞
> 
> 3 步驟
> > * 產生列序數據
> > * 產生標籤順序 `LSR`
> > * 建立一個 順序提取器 從 LSR

---

## Sequence data generation

- Label Set = {$entityS1, $entityS2, $feature}
- Three labels are used as pivots to generate
sequences.
	- Radius of 4 for optimal results
- Following words are also added
	- Distance words = {l1, l2, l3, l4, r1, r2, r3, r4}, where “li” means distance of i to the left of the pivot.
“ri” means the distance of i to the right of pivot.

	- Special words #start and #end are used to mark the start and the end of a sentence.

> 以半徑為四, 提取feature 左右兩邊的詞


**Example**

The comparative sentence
“Canon/NNP has/VBZ better/JJR optics/NNS” has $entityS1 “Canon” and $feature “optics”.

Sequences are:

```
<{#start}{l1}{$entityS1, NNP}{r1}{has, VBZ }{r2 } {better, JJR}{r3}{$Feature, NNS}{r4}{#end}>


<{#start}{l4}{$entityS1, NNP}{l3}{has, VBZ}{l2} {better, JJR}{l1}{$Feature, NNS}{r1}{#end}>
```


---

## Build a sequential cover from LSRs

LSR: 〈{*, NN}{VBZ}〉 → 〈{$entityS1, NN}{VBZ}〉

- Select the LSR rule with the highest confidence. Replace the matched elements in the sentences that satisfy the rule with the labels in the rule.
- Recalculate the confidence of each remaining rule based on the modified data from step 1.
- Repeat step 1 and 2 until no rule left with confidence higher than the minconf value (we used 90%).

> 建立 LSR cover

---

## Experimental results (Jindal and Liu, AAAI-06)

- Identifying Gradable Comparative Sentences
	- precision = 82% and recall = 81%.

- Classification into three gradable types
	- SVM gave accuracy of 96%

- Extraction of comparative relations

	- LSR (label sequential rules): F-score = 72%


--- 

## Some other work

- (Bos and Nissim 2006) proposes a method to extract items from superlative sentences. It does not study sentiments either.
- (Fiszman et al 2007) tried to identify which entity has more of a certain property in a comparative sentence.
- (Ding and Liu 2008 submitted) studies sentiment analysis of comparatives, i.e., identifying which entity is preferred.

<br>

---

---

<br>


# Review Spam

Skip


<br>

---

---

<br>

# Summary 


Two types of opinions have been discussed
  
- Direct opinions
  
  - Document level, sentence level and feature level   
  - Structured summary of multiple reviews
  
- Comparisons
  
  - Identification of comparative sentences   
  - Extraction of comparative relations
  
- Very challenging problems, but there are already some applications of opinion mining.

- Detecting opinion spam or fake reviews is very hard.






