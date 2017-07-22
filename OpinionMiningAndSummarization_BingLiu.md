# Opinion Mining & Summarization - sentiment analysis

---

## introduction - facts and opinion

<br>

### two main types of textual information.
- ## Fact 事實
- ## Opinion 意見

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
    > * 一個人或組織通常對於特定 topic 只有一項意見
    > * 意見通常會被包含在一篇文章內

---

## Find opinions on a object

**We use product reviews as an example : **

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
    > 或者系統應該提供 評論的 總結?
    
--- 

## Opinion mining - the abstraction
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
    

    