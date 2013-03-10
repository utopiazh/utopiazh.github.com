---
layout: post
title: "Notes:Practical Machine Learning in Python"
date: 2013-03-10 18:54
comments: true
categories: machinelearning 
---

Notes for video [Practical Machine Learning in
Python](http://www.youtube.com/watch?v=__s45TTXxps).


**Example: Home-runs and strikeouts predicting**

Questions:

+ What features are strong predicators for home runs and strikeouts?
+ Given a particular situation, with what probability will the batter hit a
  home run or strike out? 

**Gathering Data**

+ Get the original data
+ Coalescing
+ Scrubbing (ensure consistency)
+ Select the training data


**Select a ToolKit**

*Trade off*

+ Speed (offline or realtime)
+ Transparency (internal visibility, customizability)
+ Support (community, etc)

*Available Options:*

+ External bindings of popular packages
+ Python Implementation
  
  NLTK focus on NLP (Natural Lanaguage Processing with Python)
  mlpy
  PyML (SVM)
  PyBrain
  mdp-toolkit (abstraction over workflow)
  scikit-learn (manager algorithms, active community)

+ DIY with Bascic building blocks

  Python impl:  NumPy, SciPy
  C/C++ impl: OpenCV, LIBSVM, LIBLinear

**Feature Selection**
  
+ scikit-learn: chi-square feature selection
+ visualize significance
 

**Tips and Tricks**

+ Persistent classifier internals (save trained and reuse)
+ Using generators where possible
+ Multicore text processing (use multiple python processes)

##TODO

*chi-square*

+ [Chi-square](http://en.wikipedia.org/wiki/Chi-squared_distribution
"Chi squared distribution")

*scikit-learn*

+ [scikit-learn](http://scikit-learn.org/stable/ "scikit-learn website")
+ [scikit-learn intro video](http://www.youtube.com/watch?v=cHZONQ2-x7I
"Tutorial: scikit-learn - Machine Learning in Python with Contributor Jake
VanderPlas")
+ [SciPy-lecture](http://scipy-lectures.github.com/index.html "SciPy lecture")

*mdp-toolkit*

+ [Modular toolkit for Data Processing](http://mdp-toolkit.sourceforge.net/
"http://mdp-toolkit.sourceforge.net/")

## Reference
+ [ml-class.org](http://ml-class.org "ml-class.org")
+ [mloss.org](http://mloss.org "Machine learning open source software") 
