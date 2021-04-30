# Simple Linear Regression, Statistical Approach
#### NOTE: This tutorial follows Chapter 12 of the book "Statistics for Management" by Levin, Rubin, Siddiqui and Rastogi

We will start with a simple problem. Suppose you are in charge of an R&D facility of a company, you want to know if there is any relation between the budget of R&D per annum spent by the company and annual profit of the company. You have a feeling that there is a relationship but you don't know how to express it or how to prove it. Maybe even if there is any relation, __from where do you start investigating it? How do you know that you are approaching from the correct direction? How do you validate your approach?__ We will try to find the answers to these questions and for that let's have some data to work upon.

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

It looks like you were right all along. There is a clear relationship between annual R&D budget and annual profit, as our R&D budget is increasing our Profit is increasing too. Instead of plotting a scatter graph and try to find a relationship between two variables using our caveman eyes, we have a better way as well which is called __Chi-square test__. It tells us wheather there is a relationship but it doesn't tell us what kind of a relationship it is. As of now, we are interested in what kind of the relationship it is. We will be leaving Chi-square test for later tutorials. 
