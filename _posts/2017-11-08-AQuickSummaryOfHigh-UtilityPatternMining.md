---
layout: post
title: A quick summary of High-utility pattern mining
excerpt_separator:  <!--more-->
category: Post
---

This post is used as the notes to help me understanding the the high-utility pattern mining(HUM）. The relation resources and definitions are cut out from:

[1. A foundational approach to mining itemset utilities from databases][1]

![](https://ws1.sinaimg.cn/large/670780ffgy1flm79xa3u6j20e10aogmi.jpg)

![](https://ws1.sinaimg.cn/large/670780ffgy1flm7cznmklj20bk063aag.jpg)

* Screen shots from [[1]]

The biggest difference from apriori and HUM is the information quantity of each transaction. Which makes the ways of thinking between the two mining methods are fundamentally different.

The former method could mining the association rules of transactions based on the support-confidence model. The character allows us to ignore the larger itemsets which already contain the smaller itemset that it's support below the minimum support we expected. But this is usually not accurate enough in the cases happened in real life.

The HUM considers more details of transaction, such as the profit of items, date of purchase like the figure 2 showed. So we definitely need a new unit, utility, to calculate the associations since there are more element we need to concern. That leads the relation between the itemset k and k+1 might not the strong correlation in the utility-based system, which means the itemset k's utility lower than the minimum utility does not means the k+1 itemset should be ignored. There should be a new way to find out the relation between the itemsets.

I will cut out some useful definition below using for the futher reference. Since the following definetion indicated the rule that how utility work and the relation between different itemsets in HUM.

**Definition 2.6**. The **utility of an item** iq in a transaction Tq, denoted u(iq, Tq), is f(o(iq, Tq), s(iq)), where o(iq, Tq) is the transaction utility value of iq, s(iq) is the external utility value of iq, and f is a utility function.[[1]]

**Definition 2.8**. The **local utility** of an item xi in an itemset X, denoted l(xi, X), is the sum of the utilities of the item xi in all transactions containing X, i.e.,

![](https://ws1.sinaimg.cn/large/670780ffgy1flmd4dgu3zj208102cjrb.jpg) [[1]]

**Definition 2.9**. The **utility of an itemset** X, denoted u(X), is the sum of the local utilities of each item in X in all transactions containing X, i.e.,

![](https://ws1.sinaimg.cn/large/670780ffgy1flmd2htyg5j206n02a0sm.jpg) [[1]]

**Definition 3.3**. Let Ik = {i1, i2,...ik} be a kitemset, and let Sk−1 be the set of all subsets of Ik of size (k − 1). For a given item ip, the set Sk−1 ip = {Ik−1|ip ∈ Ik−1 and Ik−1 ∈ Sk−1} is the set of (k − 1)−itemsets that each includes ip. [[1]]

**Theorem 3.3**. (**Utility Bound Property**). The utility of an k−itemset Ik must satisfy

![](https://ws1.sinaimg.cn/large/670780ffgy1flmd7qcpc5j207602cwee.jpg) [[1]]

**Theorem 3.4**. (**Support Bound Property**). If Ik = {i1, i2,...ik} is a k−itemset and Ik−1 ip is a (k − 1)−itemset such that Ik−1 ip = Ik − {ip}, where ip ∈ Ik, then they satisfy

![](https://ws1.sinaimg.cn/large/670780ffgy1flmd92eihzj209h026mx4.jpg) [[1]]

**Theorem 3.5**. Let u(Ik) be the expected utility of Ik as described in Equation 3.7, and let u(Ik−1 1 ), u(Ik−1 2 ),...u(Ik−1k ) be the k utility values of all subsets of Ik of size (k − 1). Suppose, Ik−1 i (1 ≤ i ≤ m) are high utility itemsets, and Ik−1 i (m + 1 < i ≤ k) are low utility itemsets. Then

![](https://ws1.sinaimg.cn/large/670780ffgy1flmdbf8fr7j20fj05w74x.jpg) [[1]]

  [1]: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.70.53&rep=rep1&type=pdf
