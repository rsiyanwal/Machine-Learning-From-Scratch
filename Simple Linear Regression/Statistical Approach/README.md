# Simple Linear Regression, Statistical Approach
#### NOTE: This tutorial follows Chapter 12 of the book "Statistics for Management" by Levin, Rubin, Siddiqui and Rastogi

We will start with a simple problem. Suppose you are in charge of an R&D facility of a company, you want to know if there is any relation between the budget of R&D per annum spent by the company and annual profit of the company. You have a feeling that there is a relationship but you don't know how to express it or how to prove it. Maybe even if there is any relation, __from where do you start investigating it? How do you know that you are approaching from the correct direction? How do you validate your approach? and can you predict the profit in upcoming years if you have the value of the budget for R&D?__ We will try to find the answers to these questions and for that let's have some data to work upon.

| Year | Amount Spent on R&D | Annual Profit  |
|------|------------|-------------|
| 1990 | 2 | 20 |
| 1991 | 3 | 25 |
| 1992 | 5 | 34 |
| 1993 | 4 | 30 |
| 1994 | 11 | 40 |
| 1995 | 5 | 31 |

(in millions)

Now, there is a question, __does the year have any impact on the problem that we are working on?__ Our problem is about the relation between the R&D budget and the Profit but we are not concerned about the year. Maybe in some different problem we want to know if there is any relationship between the year and the profit and maybe we find some relation too, but for now we are only concerned with R&D budget and the Profit. Hence, we will only deal with just these two features and our data should look like this --

| Amount Spent on R&D | Annual Profit  |
|------------|-------------|
| 2 | 20 |
| 3 | 25 |
| 5 | 34 |
| 4 | 30 |
| 11 | 40 |
| 5 | 31 |

(in millions)

This is an opportuinity to understand what are __Dependent Variable__ and __Independent variable__. Let's recall our problem, we want to know if there is any relationship between ammount spend on R&D and Profit of the company on annual basis. What are we inffering? We are thinking that if we increase the budget of R&D per annum then our annual profit may increase and if we decrease our R&D budget per annum then our annual profit will decrease. Here, __Annual Profit__ is a Dependent Variable because it depends on the value of budget of R&D. Whereas, __Amount Spent on R&D__ is an Independent variable because we are assuming that its value is not depending upon the value of any other variable. 

It doesn't mean that __Amount Spent on R&D__ is inherently an independent variable. If our problem statement was different and we wanted to know if our budget of R&D has incresed or decreased per year then __Amount Spent on R&D__ would have been dependent variable and __Year__ would have been an independent variable. 

**_In Machine Learning, we can only have one Dependent Variable but we can have more than one Independent Variables._**  

Moving on, we have a gut feeling that there is a relation between the budget of R&D and the annual profit but where do we start investigating it? Maybe, we should start by plotting a graph, a scatter plot would be nice. 

    # -- Importing the Libraries --
    import matplotlib.pyplot as plt

    # -- Defining X and Y --
    x = [2, 3, 5, 4, 11, 5]
    y = [20, 25, 34, 30, 40, 31]

    # -- Plotting --
    plt.xlabel("Amount Spent on R&D")
    plt.ylabel("Annual Profit")
    plt.scatter(x, y)
    plt.show()

![R D Annual Profit](https://user-images.githubusercontent.com/11557572/116685830-956a5e80-a9d0-11eb-9399-26b77c2052a1.png)

It looks like you were right all along. There is a clear relationship between annual R&D budget and annual profit, as our R&D budget is increasing our Profit is increasing (Direct Relationship). Instead of plotting a scatter graph and try to find a relationship between two variables using our caveman eyes, we have a better way as well which is called __Chi-square test__. It tells us wheather there is a relationship but it doesn't tell us what kind of a relationship it is. As of now, we are interested in what kind of the relationship it is. We will be leaving Chi-square test for later tutorials. 

The relationship can either be a positive one or a negative one. The positive one is called as __Direct Relationship__ in which the value of dependent variable increases are value of independent variable increases. Another one which represents a negative relationship is called __Inverse Relationship__ in which the value of dependent variable decreases as the value of independent variable increases.  

![DirectRelationship](https://user-images.githubusercontent.com/11557572/116692808-94d6c580-a9da-11eb-8d0f-907b0e38be41.png)        ![InverseRelationship](https://user-images.githubusercontent.com/11557572/116692485-0d895200-a9da-11eb-918e-35dc326d9fe7.png)

The type of relationship we are studying here is called __Regression__ (in which there can exist either a direct relationship or an inverse relationship) but what is Regression? 

> The term regression was first used as a statistical concept in 1877 by Sir Francis Galton. Galton made a study that showed that the height of children born to tall parents tends to move back, or "regress," towards the mean height of the population. _He designated the word __regression__ as the name of the general process of predicting one variable (the height of the children) from another (the height of the parent)_. -- Statistics for Management, Page number 596

__The Regression can also be of many types, they are as follow:__

![Types_of_Regression](https://user-images.githubusercontent.com/11557572/116693574-c0a67b00-a9db-11eb-87df-965685949fd5.png)


As you may have notices by now, we are learning Simple Linear Regression and so we will be dealing with Direct Linear Regression and Invesrse Linear Regression. The word "Simple" in Simple Linear Regression means that we are only considering two variables (or features). 

Regression is used for prediction. We are trying to predict the annual profit on the basis of amount spent on R&D. Linear Regression tries to predict the dependent variable by __"fitting"__ a __straight line__ between the scattered points. Later on, a point on the straight line given on some value of independent variable is called as __Estimated Value or Predicted Value__. For Example, examine the graph below in which a Regression line (in pink) is already implemented

![DirectRelationPredicted (1)](https://user-images.githubusercontent.com/11557572/116697485-dcf8e680-a9e0-11eb-9a91-ee79347aea4b.png)

In this graph, x-axis represents independent variable and y-axis represents dependent variable. For the value 6 of independent variable, our Actual Value (blue line) is between 15 to 20 whereas our Estimated or Predicted value (black line) by our Regression Line is between 20 to 25. If thi was the graph of our R&D budget and Annual Profit problem, it would have meant that our actual profit is between 15 to 20 million at R&D budget of 6 million. Whereas, our prediction is telling us that our profit is between 20 to 25 million at R&D budget of 6 million.  

### A Regression Line
A simple line in 2D plane is represented by the equation __Y = a + bX__ where __a__ is the y-intercept and __b__ is a slope. 
To understand the regression line we need to undestand what Y and X are and what "a" and "b" are. X is the Independent Variable, Y is the Predicted Value, a is the point at which the regression line intercepts the y-axis and b is the slope. 

Let's talk about y-intercept or a. We are putting b = 0 so that the line is parallel to x-axis. "a" is the value at which the regression line intercepts the y-axes. If a = 1 then the regression line will cross at y = 1 and if a = 5 then the regression line will cross at y = 5. Below is the graph depicting a at the various values between -2 and 4.

![y-intercept](https://user-images.githubusercontent.com/11557572/116717860-fc9b0980-a9f6-11eb-9d81-6b1caf7f3dcb.gif)

If we put a = 0 (which means the line intercepting the y-axis is at y = 0), then we can see how b is working as a slope. In the graph below the value of b is ranging from -10 to 10. If b = 0 then the regression line is parallel to x-axis, if b = 1 then the regression line will intercept the point (1, 1) and if b = 6 then the regression line will intercept at the point (1, 6).

![slope](https://user-images.githubusercontent.com/11557572/116714957-e3448e00-a9f3-11eb-9a3b-8ee927c561ed.gif)

You can notice that if the value of a = 0 and the value of b = 2 then the regression line will pass through the points (0, 0) and (1, 2).

![RegressionLineExample1](https://user-images.githubusercontent.com/11557572/116720381-bdba8300-a9f9-11eb-906d-53ed44a7e264.png)

and if a = 1.5 and b = 0.5

![RegressionLineExample2](https://user-images.githubusercontent.com/11557572/116735543-493d0f80-aa0c-11eb-9747-6343e310f893.png)

Therefore, __if the value of y-intercept is "a" and the value of the slope is "b" then the regression line will pass through the points (0, a) and (1, b + a)__.

### What to do with a Regression line, actual values and predicted values?
We are going to find that regression that fits our data the best. And we validate the fitness of our regression line by using __Least-square error__. Our original data is 

| Amount Spent on R&D | Annual Profit  |
|------------|-------------|
| 2 | 20 |
| 3 | 25 |
| 5 | 34 |
| 4 | 30 |
| 11 | 40 |
| 5 | 31 |

(in millions)

And we need to predict the value of dependent variable as accurately as possible. The values of a and b can vary and depending upon the decimal value of a and b we are taking, there can be millions of combinations. Here is the scatter plot of the data we are working on and few examples of regression lines..

![variousRegressionLines](https://user-images.githubusercontent.com/11557572/116736740-ea789580-aa0d-11eb-8bb0-7c4bf51bf200.png)

We need to find a way to judge these lines and figure out which one is the best and least-square error helps us with that. Let's take one example as see how least-square error works. 

| Y | Y'| (Y - Y')^2 |
|---|---| ---------- |
| 4 | 5 | 1 |
| 7 | 4 | 9 |
| 2 | 3 | 1 |
|---|---|Sum = 11|

In the example above, the sum of squares of the Predicted Values (Y') subtracted from Actual Values (Y) is 11. The example may have used some values of a and b and evaluated Predicted Value (Y') for each of the data points. If we have tens of thousands of values for a and b then we will have that many 
