---
title: "Accessing list object in Rcpp using RcppArmadillo"
author: "Zikai Lin"
date: "1/12/2021"
categories:
  - blog
tags:
  - R
  - Rcpp


---



## Accessing list object in Rcpp using RcppArmadillo.



### Create a list object in Rcpp

In Rcpp, you can create a list of object by using `List::create()` function. The name of element can be created using either `Rcpp::Named()` or `_[]`.

```cpp
// Create list L from vector v1, v2
List L = List::create(v1, v2);

// When giving names to elements
List L = List::create(Named("name1") = v1 , _["name2"] = v2);
```



### Accessing the elements in list

You can easily access the element in a list by either using indices or character name.

```cpp
NumericVector v1 = L[0];
NumericVector v2 = L["V1"];
```

However, notice that the objects in list are stored in `Rcpp::Vector` form, therefore, if you are using `RcppArmadillo`, you need to convert it to `arma::mat` :

```cpp
arma::mat v1_mat = as<arma::mat>(L[0]);
arma::mat v2_mat = as<arma::mat>(L["V1"]);
```

