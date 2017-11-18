---
layout: post
title: A quick view of HUM alg. in today
excerpt_separator:  <!--more-->
category: Post
---

Last post is the definitions that why the High-Utility Mining(HUM) works. This post will become a reference for me to get a overview of HUM in 2017. This is a summary of the paper:

[1. A Review of Mining High Utility Patterns][1]

First, the paper indicated that a HUM alg. has following steps:

![](https://ws1.sinaimg.cn/large/670780ffgy1flmdradpuvj20hz04ogm0.jpg)

The idea is simple, find out the all combinations of items, which becomes the itemsets we called in the DM area. Then calculate the utility of each itemsets and show the itemsets whose utility higher than the min.util.

But this remains me a question I asked before: how to find the itemsets out efficiently and how to calculate the utility of each itemsets efficiently? The cluster might be a solution, since the map reduce can provide the power to support the hugh calculation, and I know that is one of the advantage of Spark. But is there a way to optimize the reading speed? If the data has hundred million of items, can I improve the processing speed of my alg.?

Actually the paper I read of last post anwsered my second question. There is an equation to show the relations of utilities between each I can try to use to reduce the calculations of utilities. And I am going to check that is there an exist technique that I could use for my first question.

There are three pre-request alg. that are usually used in the HUM:
**1. Depth first algorithm
2. Breadth first algorithm
3. Hybrid algorithm**
Fortunately, I do have some experiences of those alg.s since the competition I attended. And there are 11 HUM alg.s showed in below(I will only list out the pro. and con.):

**1. Pseudo Projection**
This work build tree-based pseudo projections and array-based unfiltered projections has been build for projected transaction subsets which makes algorithm both CPU time efficient and memory saving. The disadvantage of this algorithm is, it only support minimum description code length with **small number of patterns**.

**2. Frequent Pattern Growth (FP-Growth)**
The alg. that mentioned in the COMP4710.
Pro: Saved in the subsequent mining processes. Also this work shrink the database scanned in each pass and it takes more computation time.
Con: it reduces multipass candidate generation process in the first phase by **discarding isolated items** to reduce the number of candidates.


**3. Two-Phase**
Pro:  This algorithm requires fewer database scans, less memory space and less computational cost
Con:  The insufficient frequent counts for repeated candidate itemset which can **lose interesting patterns**


**4. Isolated Items Discarding Strategy (IIDS)**
Pro: This algorithm discovered high utility itemset with less number of candidates which improve the performance of the pattern mining.
Con: still suffers with the problem of level wise generation and test problem of apriori and it **requires multiple database scans**.

**5. Transaction Weighted Utility (TWU)**
Pro: In this work the task of high utility itemset mining discovers all the utility which has utility higher than the user specifiedutility.
Con: Generation of frequent graphs results in **high in memory** usage and **low in accuracy**.

**6. Fast Utility Mining (FUM)** (Looks good?)
Pro:  This algorithm provides absolute accuracy and proves to be extremely efficient in finding every possible high utility itemset from the transactions in the database, also efficiently handles the duplicate itemsets.

**7. Incremental High Utility Pattern Mining (IHUPM)**
Pro:  It does not require any restructuring operation even when the data base is incrementally updated. They have achieved the less memory consumption.

**8. Utility Pattern Growth Plus (UP-Growth+)**
The estimated utilities of candidates are well reduced, by discarding the utilities of the items which are impossible to be high utility or not involved in the search space.
Pro: This algorithm outperforms substantially in terms of execution time, especially when the database contains lots of long transactions.
Con: However the operation time and search space of high-utility itemset mining can increase the high computation cost.

**9. High Utility Itemset Miner (HUI-Miner)**
Pro:  This algorithm first estimate the utilities of the itemsets and generate the candidate itemsets and then by scanning the database compute the exact utilities of the itemset to generate the high utility itemset. This algorithm mines the high utility itemset without generation of the candidates and the algorithm outperforms in terms of both running time and memory consumption.


**10. Faster High-Utility Miner (FHM)**
Pro: This algorithm is up to 6 times faster than high utility itemset miner.
Con: It assumes that each item cannot appear more than once in each transaction and that all items have the same importance.

**11.  Direct Discovery of High Utility Pattern (D^2HUP)**
Pro: This algorithm addresses the scalability and efficiency issues occurred in the existing systems as it directly extracts the high utility patterns from large transactional databases.

[1]: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.70.53&rep=rep1&type=pdf
