---
layout: post
title: "Learning to Count I: Combination & Permutation Trees"
usemathjax: true
category: Mathematics
tags: discrete-math permutation combination trees
---

Here I offer a slightly different perspective on permutations and combinations,
which give us a simple way to write algorithms to generate them.
This post is split into 3 parts:
here I explain how to generate the trees and the rules
defining them; part II derives traditional
formulas; and finally part III will present
a simple implementation.

Say we have 4 items $$S=\{a,b,c,d\}$$,
how many different ways can we take 3 items from $$S$$?

This is an ambiguous question,
first we can establish:

 * Do choosing the same items in a different order result in different choices?
 * Can we take the same item more than once?

This breaks the question into 4 types:
<table>
  <tr>
    <th></th>
    <th>Order</th>
    <th>No Order</th>
  </tr>
  <tr>
    <th>Repetition</th>
    <td>Permutation with repetition</td>
    <td>Combination with repetition</td>
  </tr>
  <tr>
    <th>No Repetition</th>
    <td>Permutation without repetition</td>
    <td>Combination without repetition</td>
  </tr>
</table>

We can now answer the question in the four cases.
Each time, we consider a systematic approach to generating the different
options,
which are visualised using trees.
These trees give a clear way to compare different cases,
and suggest that a recursive algorithm could generate them.

## Permutations with Repetition

Here we count different orders, and we can take the same object twice.

We can imagine trying to fill three slots _ _ _
where each slot can take any of $$\{a,b,c,d\}$$.

$$aaa,aab,aac,aad,aba,abb,abc,abd,aca,acb,\dots$$

This is easily visualised as a tree,
where each path to a leaf node corresponds to a different
option.

<figure>
    <img src="/img/permutation-trees/perm1.jpg" class="custom-image">
    <figcaption style="text-align: center;">
        Permutation tree with highlighted paths \(\color{red}{bcc}\) and \(\color{green}{daa}\)
    </figcaption>
</figure>

## Permutations without Repetition

Continue to count different orders, but remove any repetition.

Similar to before, we could imagine three slots _ _ _ and fill them with
items from $$\{a,b,c,d\}$$. However once we fill the first slot to get
$$x$$ _ _, we cannot use $$x$$ again. This happens every time
leaving one less item available the next slots.

$$abc,abd,acb,acd,adb,adc,bac,bad,bca,bcd\dots$$

Again this is a tree; no path to a leaf in this tree can contain the same
node twice.

<figure>
<center>
    <img src="/img/permutation-trees/perm2.jpg" class="custom-image" >
    <figcaption>
        Permutation tree with highlighted paths \(\color{red}{abc}\) and \(\color{green}{cbd}\)
    </figcaption>
</center>
</figure>

## Combinations with Repetition

Now we reinstate the ability to pick the same object twice,
but stop counting different orders as different outcomes.

The most common way people go about generating these is to
consider all combinations with three $$a$$'s, then with two a's, then with 1 $$a$$, and finally with no $$a$$'s.

$$aaa,aab,aac,aad,abb,abc,abd,acc,add,bcd,\dots$$

The tree picture now must have the property that no two paths
use the same letters.
When drawing the tree,
no parent's children "left" of the current node should
appear in current node's descendants.

<figure>
<center>
    <img src="/img/permutation-trees/comb1.jpg" class="custom-image" >
    <figcaption>
        Combination tree with highlighted paths \(\color{red}{aac}\) and \(\color{green}{bbd}\)
    </figcaption>
</center>
</figure>

## Combinations without Repetition

Now we can remove repetition to get the a traditional
combination.
This tree can be obtained by applying the two rules used above:
1. Disallow a path to use the same node more than once
2. Prevent descendants containing left siblings

<figure>
<center>
    <img src="/img/permutation-trees/comb2.jpg" class="custom-image" >
    <figcaption>
        Combination tree with highlighted paths \(\color{red}{aac}\) and \(\color{green}{bbd}\)
    </figcaption>
</center>
</figure>

# Conclusion

These trees can be boiled down to
two rules which determine how the tree is generated.

* (A) Parents cannot contain any ancestors
* (B) Descendants cannot contain left siblings

Which can be tabulated as follows.

<table>
  <tr>
    <th></th>
    <th>Order</th>
    <th>No Order</th>
  </tr>
  <tr>
    <th>Repetition</th>
    <td>No rules</td>
    <td>(A)</td>
  </tr>
  <tr>
    <th>No Repetition</th>
    <td>(B)</td>
    <td>(A) and (B)</td>
  </tr>
</table>

Each application of a rule reduces
(or keeps equal) the number of nodes in a tree,
leading to the subset relations visualised below.

<figure>
<center>
    <img src="/img/permutation-trees/subset.jpg" class="custom-image" >
    <figcaption>
        Subset relation between trees visualised for example of taking 3 elements
        from 4.
    </figcaption>
</center>
</figure>

