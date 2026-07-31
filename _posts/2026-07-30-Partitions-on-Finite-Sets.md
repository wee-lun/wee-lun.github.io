---
layout: post
title: Ordering of Partitions on Finite Sets
date: 2026-07-30 19:29:30+0800
description: We try to give a (unnecessary) formalization that the collection of all partitions on a given finite set as a category, after invoking a partial order on it.
tags: category, topology, partitions, combinatorics
categories: math
toc:
  sidebar: left
---

<div align="justify" markdown=1>
This post is inspired from Aluffi's *Algebra: Chapter 0*. In the book, readers are asked to proved that there is a one-to-one correspondence between a partition of a finite set $S$ and an equivalence relation of a finite set $S$. 

Indeed, an equivalence relation implies a partition of set $S$, since the equivalence classes is a disjoint union. Conversely, given a partition of $S$, we define equivalence relation $a\sim b$ if and only if both $a$ and $b$ are contained in the same block. The details could be easily verified, thus omitted here.

However, we could have more structure in the partitions. This writing demonstrate some simple and unnecessary yet interesting formalization of partitions involving defining a monoid structure from a partition, an ordering for different partitions, and therefore building us a category of partitions of a finite set. 

<!--more-->

## **Partitions and Monoid**

Let $S$ be a finite set, and let $\mathcal P=\\{ P_i\\}_{i=1}^n$ be a partition of $S$, where we denote each block as $P_i$. To make a monoid out of $P$, we first need a binary action, specifically a binary action of *sets*. A good candidate is union. However, all these quickly breakdown to two problems:

1. There is no identity element, i.e. an element $\mathrm{id}\in \mathcal P$ such that for every $A\in \mathcal P$ we have

$$A\cup \mathrm{id} = \mathrm{id}\cup A= A$$ 

2. We need not have closure. Consider a partition $\mathcal P:=\\{\\{1\\\}, \\{2\\\}, \\{3\\\}\\\}$ on $\\{1,2,3\\\}$. Immediately we see the union of any two distinct elements of $P$ is not an element of $P$.

The first issue can be solved easily by simply introducing $\emptyset$ as the identity element. For the second issue, necessity of closure forces us to include *all* the possible union. Therefore, a monoid induced by the given partition $\mathcal P$ has the set of objects:

$$M_{\mathcal P}:=\left\{\bigcup_{i\in I} P_i: I\subseteq \{1, \dots, n\}\right\}$$

Note that the monoid is automatically a topology. It suffices to see that closure of intersection is satisfied. Suppose given $a,b\in M_{\mathcal P}$. By definition of $M_{\mathcal P}$ we know there exists index sets $r,s\subseteq\\{1,\dots,n\\}$ such that

$$a=\bigcup_{i\in r} P_i \quad \text{and} \quad b=\bigcup_{j\in s}P_j$$

Since the blocks $P_i$ are disjoint, so any intersection must result in complete blocks. This implies that the intersection is

$$ a\cap b = \bigcup_{i\in r\cap s} P_i$$

Since $r\cap s\subseteq \\{1,\dots,n\\}$, so $a\cap b$ must be an element of $M_{\mathcal P}$, by definition. 

The topological structure of $M_{\mathcal P}$ is more or less another perspective to see the monoid. It could be connected back to the big picture by seeing that the connected components of $M_{\mathcal P}$ in terms of topology is exactly the partition $\mathcal P$.

## **Ordering of Partitions**

We have constructed a monoid induced by a given partition. We can use this to define a partial order on *the family of all possible partitions of $S$*. Suppose given two partitions $\mathcal P$ and $\mathcal Q$ of $S$. We define the ordering

$$\mathcal P \preceq \mathcal Q \iff M_{\mathcal Q} \subseteq M_{\mathcal P}$$

It is easy to verify that the above definition is indeed a partial order, where one could verify the three axioms of partial order directly, i.e. reflexivity, antisymmetry, and transitivity. On the other hand, since $M_\mathcal P$ and $M_\mathcal Q$ are topologies $\tau_{\mathcal P}$ and $\tau_{\mathcal Q}$ respectively, the definition of the partial order is a relabel of the comparison of topologies.

The definition above is also equivalent to the following, which doesn't required the notion of monoid. We define $\mathcal P\preceq \mathcal Q$ if and only if for every block $P_i\in \mathcal P$ can be written as a union of blocks of $\mathcal Q$. 

Thus, in plain language, we are saying that *$\mathcal P$ is finer than $\mathcal Q$*. Also, it is not difficult to see that the 'largest' partition would therefore be $\\{\\{S\\}\\}$ and the 'smallest' (non-trivial) partition will be $\\{\\{s\\}:s\in S\\}$. It is also clear that not all partitions are comparable. For example, these two partitions $\\{\\{1,2\\},\\{3,4\\}\\}$ and $\\{\\{1,4\\},\\{2,3\\}\\}$ are not comparable. 

## **Categories from the Partial Order**

It is well-known that a partial order induces a category, in particular a [skeletal thin category](https://en.wikipedia.org/wiki/Thin_category) Thus, the partial order $\preceq$ we defined previously defined a category, or, to be precise, three equivalent categories:
1. The category $\Pi(S)$ of partitions of $S$,
2. The category $\mathrm{Mon}\Pi(S)$ of monoids induced by partitions of $S$, and
3. The category $\mathrm{Top}\Pi(S)$ of topology induced by partitions of $S$.
where the isomorphisms are given by

$$\mathcal P \mapsto M_{\mathcal P} \mapsto \tau_{\mathcal P}$$

To be more specific, tha map $\mapsto M_{\mathcal P} \mapsto \tau_{\mathcal P}$ is order-perserving, whilst if compared to $\mathcal P$ both are order-reversing. To be specific, we have the relationship

$$\mathcal P \preceq \mathcal Q \iff M_{\mathcal P}\supseteq M_{\mathcal Q} \iff \tau_{\mathcal P} \supseteq \tau_{\mathcal Q}$$

Note that there is another category which is also equivalent to the above-listed, however I want to reserve it as the last section of this writing.  

## **Category of Equivalence Relation**

Upon some searching, I found that people has dicussed that how can [equivalence relations be formalized via category](https://math.stackexchange.com/q/1667749), however there was no discussion on how *equivalence relations can form a category* (perhaps because it was unnecessary, but I think it's interesting).

Given an equivalence relation $R$ on set $X$, we can express the relation in set as follow:

$$\mathcal E_{R} := \{(a,b) \in X\times X:aR b\}$$

We then say that the equivalence relation $R$ is represented by $\mathcal E_{R}$. So, for example, an equivalence relation (given by equivalence classes) $\\{\\{1,2\\},\\{3,4\\}\\}$ is represented by

$$\{(1,1),(1,2),(2,1),(2,2),(3,3),(3,4),(4,3),(4,4)\}$$

Suppose given two equivalence relations ${R_1}$ and ${R_2}$, their *intersection* $R_1 \cap R_2$ is given by the equivalence relation represented by $\mathcal E_{R_1} \cap \mathcal E_{R_2}$. The intersection of equivalence relations then defines a partial order, where 

$$R_1\leq R_2 \iff R_1 \cap R_2 = R_1$$

Again, we omit all the verification. For example, given the equivalence relations (represented by equivalence classes)

$$R_1:=\{\{1\},\{2\},\{3\},\{4\}\} \quad \text{and} \quad R_2:= \{\{1,2\},\{3,4\}\}$$

we see $R_1\cap R_2 = R_1$, thus $R_1\leq R_2$. This agrees with the previous section where $\\{\\{1\\},\\{2\\},\\{3\\},\\{4\\}\\}$ is the finest, in terms of ordering of partitions. Broadly speaking, in two settings we have the correspondence where 'finer' $\leftrightarrow$ 'smaller' and vice versa.

With the defined partial order, we can therefore define category of equivalence relation $\mathrm{Eq}(S)$ on set $S$. As one expected, this category is equivalent to the three categories previously listed, and the isomorphism is exactly the bijective correspondence between a partition and an equivalence relation we worked out earlier.

## Before Ending

I do aware that there is a wider relationship of the mentioned topic to lattice theory. Unfortunately, I have no exposure towards the theory, even the basics. Again, as stressed as the beginning, much of these are probably unnecessary rigor since these are merely *a change of vocabulary* instead of deriving any new things. But I am always happy to see more examples of categories, and I am satisfied for now.  

</div>
