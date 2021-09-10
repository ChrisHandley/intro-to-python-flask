---
layout: lesson
root: .
permalink: index.html
---

The best way to learn how to program is to do something useful,
so this introduction to Python is built around a common scientific task:
**data analysis**.

### Molecular Features
We are studying **molecular features** for similar molecules to find correlations and
make predictions about reactions based upon their properties.

There are 343 molecules, each with 17 features of interest 
and a further value which is a measure of the preference of the reaction.

To see how these properties are correlated we will;

1. Calculate the average property for each across the set. 
2. Plot the correlation between the properties.


### Data Format
The data sets are stored in
[comma-separated values]({{ page.root }}/reference.html#comma-separated-values) (CSV) format:

- each row holds information for a molecule,
- columns represent a property.

The first three rows of our first file look like this:
~~~
,%top,ER1,ER2,ER3,ER4,ER5,ER6,ER7,EZ,LMW,LVR1,LVR1+4,LVR1+4/3+6,LVR2,LVR3,LVR3+6,LVR4,LVR5,LVR6,LVR7,LVWhole,RS,Rh source,SStoutR1,SStoutR2,SStoutR3,SStoutR4,Type,VB,boron reagent,equivs boron reagent,ligand,mol% Rh,mol% ligand,solvent,substrate,temp,time,yield
0,6,-0.09,0,0,-0.09,0,0,0,0,272.1565006,94.18429025,188.3685805,188.3685805,0,0,0,94.18429025,0,0,20.25598522,279.4546413,1,[Rh(C2H4)2Cl]2,22.51198396,21.5742147,0,0,Lam,348.0319373,B1(C2=CC=CC=C2)OB(C3=CC=CC=C3)OB(C4=CC=CC=C4)O1,2,L3.1,1.5,3,dioxane,O=C1C=CCC1,50,1,88
1,2.333333333,-0.09,0,0,-0.09,0,0,0,0,272.1565006,94.18429025,188.3685805,188.3685805,0,0,0,94.18429025,0,0,20.25598522,279.4546413,1,[Rh(C2H4)2Cl]2,22.51198396,19.43509996,0,0,Lam,134.6239983,OB(O)C1=CC=CC=C1,2,L3.1,1.5,3,dioxane,O=C1C=CCCC1,30,1,94
~~~
{: .source}
The first row are the headers of our data, the labels.

The subsequent rows represent the values for each entry for each of those lables.

For example, for entry 1, the id of this entry is 0 - the first value of the row, and the %top is 6.

In order to analyze this data, do some machine learning, and report to our colleagues, we'll have to learn a little bit
about programming.

> ## Prerequisites
>
> You need to understand the concepts of **files** and **directories** and how to start a Python
> interpreter before tackling this lesson. This lesson sometimes references Jupyter
> Notebook although you can use any Python interpreter mentioned in the [Setup][lesson-setup].
>
> The commands in this lesson pertain to **Python 3**.
{: .prereq}

### Getting Started
To get started, follow the directions on the "[Setup][lesson-setup]" page to download data
and install a Python interpreter.

{% include links.md %}
