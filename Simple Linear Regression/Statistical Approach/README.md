# Simple Linear Regression, Statistical Approach
#### NOTE: This tutorial follows Chapter 12 of the book "Statistics for Management" by Levin, Rubin, Siddiqui and Rastogi

Let's consider a dataset that includes the annual budget spent by the company on R&D and the corresponding annual profit made by the company. We can start by visualizing this data and checking if there is any pattern or trend in the data. We can use statistical techniques like correlation analysis and regression analysis to determine if there is a relationship between the two variables.

To validate our approach, we can use cross-validation techniques and measure the performance of our model on unseen data. We can also use hypothesis testing to check the significance of our findings.

If we have a model that can predict the profit based on the budget spent on R&D, we can use it to make predictions for upcoming years. However, we should keep in mind that the accuracy of our predictions may vary based on various factors like changes in the market, competition, economic conditions, etc.

| Year | Amount Spent on R&D | Annual Profit  |
|------|------------|-------------|
| 1990 | 2 | 20 |
| 1991 | 3 | 25 |
| 1992 | 5 | 34 |
| 1993 | 4 | 30 |
| 1994 | 11 | 40 |
| 1995 | 5 | 31 |

(in millions)

We need to ask ourselves whether the year has any influence on the problem at hand. Our task is to examine the connection between the R&D budget and the profit, and we are not interested in the year. Although in a different problem, we may be interested in discovering any association between the year and the profit, and we may even identify one. However, for now, we are solely interested in the R&D budget and the profit. Therefore, we will only consider these two features, and our data should appear as follows --

| Amount Spent on R&D | Annual Profit  |
|------------|-------------|
| 2 | 20 |
| 3 | 25 |
| 5 | 34 |
| 4 | 30 |
| 11 | 40 |
| 5 | 31 |

(in millions)

In order to understand the concepts of Dependent Variable and Independent Variable, let us consider our problem statement. We want to determine whether there is a relationship between the amount spent on R&D and the annual profit of a company. Our assumption is that increasing the budget for R&D per annum may lead to an increase in annual profit, and decreasing the budget may lead to a decrease in annual profit. Here, Annual Profit is the dependent variable as it depends on the value of the R&D budget. On the other hand, Amount Spent on R&D is the independent variable as its value is not influenced by any other variable.

It is important to note that the independence or dependence of a variable is not inherent, but depends on the specific problem being studied. For instance, if we wanted to determine whether the budget for R&D has increased or decreased per year, then Amount Spent on R&D would be the dependent variable and Year would be the independent variable.

In machine learning, we typically have one dependent variable and one or more independent variables. To investigate whether there is a relationship between the R&D budget and annual profit, we can start by plotting a scatter plot.

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

In the example above, the sum of squares of the Predicted Values (Y') subtracted from Actual Values (Y) is 11. The example may have used some values of a and b and evaluated Predicted Value (Y') for each of the data points. If we have tens of thousands of values for a and b then we will have that many __hypothesis__ to check. 

A set of hypothesis to try may look like this: 

1. Y = 0.1 + 0.1X
2. Y = 0.1 + 0.2X
3. Y = 0.1 + 0.3X
4. Y = 0.2 + 0.1X
5. Y = 2.1 + 0.3X
(...and many more)

Of course, we can't go through all the millions of cobinations of a and b because that's not feasible, instead __Statistical Approach__ gives us two formulae to calculate the values of a and b on which we will have the minimum least-square error out of all the hypothesis. 

![slopeFormula](https://user-images.githubusercontent.com/11557572/116779688-61a53c80-aa95-11eb-8f37-1677020b3f3b.png)

![y-intercept](https://user-images.githubusercontent.com/11557572/116779835-4d157400-aa96-11eb-8b61-9d45a4090a26.png)

![formulae](https://user-images.githubusercontent.com/11557572/116782764-a090bd80-aaa8-11eb-9d85-a2abfdc66303.png)

Alright, so since we have the formulae and we have an understanding of why we need to use them, let's write a code and implement a __Simple Linear Regression using Statistical Approach__

__Defining the Data:__

            # -- We are denoting Independent Variable as x2 and Dependent Variable as y2 --
            x2 = [11, 10, 8, 5, 9, 9, 7, 3, 11, 8, 7, 2, 9, 8, 6, 3]
            y2 = [40, 31, 26, 16, 39, 32, 20, 14, 35, 28, 26, 11, 36, 29, 17, 18]
          
__Performing the Least-square method:__

            # -- Mean of the values of Independent Variables --
            sum = 0
            for i in x2:
              sum = sum + i
            len_x = len(x2)
            mean_x = sum / len_x
            print("Mean of Independent Variable: ", mean_x)
           
            # -- Mean of the values of Dependent Variables --
            sum = 0
            for i in y2:
              sum = sum + i
            len_y = len(y2)
            mean_y = sum / len_y
            print("Mean of Dependent Variable: ", mean_y)
            
            # -- Sum of X*Y --
            sum_xy = 0
            xy_list = []
            for i in range(0, lengthX - 1):
              xy_list.append(x2[i] * y2[i])
            print(xy_list)
            for i in range(0, lengthX - 1):
              sum_xy = sum_xy + xy_list[i]
            print("Sum of xy is: ", sum_xy)

            # -- n * mean_x * mean_y --
            n_mean_x_mean_y = len(x2) * mean_x * mean_y
            print(n_mean_x_mean_y)

            # -- Sum of square of the values of independent variable --
            sum_sq_x = 0
            sq_x = []
            for i in range(0, lengthX):
              sq_x.append(x2[i] ** 2)
            print("sq x: ", sq_x)
            for i in range(0, lengthX):
              sum_sq_x = sum_sq_x + sq_x[i]
            print(sum_sq_x)

            # -- square of the mean of dependent variable * n --
            n_mean_x_sq = len(x2) * (mean_x ** 2)
            print(n_mean_x_sq)

            # -- Slope (b) of the regression line --
            b = (sum_xy - n_mean_x_mean_y)/(sum_sq_x - n_mean_x_sq)
            print("Slope(b or m) of the regression line is: ", b)

            # -- y-intercept (c) of the regression line is --
            a = mean_y - b * mean_x
            print("Y-intercept (a or c) is: ", a)

__Drawing a Regression Line:__

            # -- Importing the Libraries --
            import matplotlib.pyplot as plt
            
            # -- Drawing regression line --
            x3 = []
            y3 = []
            for i in range(2, 12):
              x3.append(i)
            for i in range(0, 10):
              y3.append((b * x3[i]) + a)

            print(x3)
            print(y3)
            # -- Plotting --
            plt.scatter(x2, y2, c = '#88c999')
            plt.plot(x3, y3, c = 'hotpink')
            plt.title("Simple Linear Regression")
            plt.show()


![SLR](https://user-images.githubusercontent.com/11557572/116783822-91ad0980-aaae-11eb-987b-7b2325293a78.png)

We have understood how to perform Simple Linear Regression using Statisitcal Approach. In our next topic we will discuss how to perform Simple Linear Regression using __Gredient Descent Method__.



