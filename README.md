# CarseatsDataset_R_Analysis
Dataset Carseats contains the information about 400 carseats. Data are included in
package ISLR.

upload library ISLR

library(ISLR)

and the dataset
data(Carseats)

dimension of the data
dim(Carseats)
 [1] 400 11
variables

names(Carseats) <br>
[1] "Sales" "CompPrice" "Income" "Advertising" "Population" "Price" <br>
[7] "ShelveLoc" "Age" "Education" "Urban" "US"

Extract the variables of interest, namely, Sales, Price, Urban, US, ShelveLoc.

my.data <- Carseats[, c('Sales', 'Price', 'Urban', 'US', 'ShelveLoc')]<br>
my.data[1:3,]

Sales Price Urban US ShelveLoc
1 9.50 120 Yes Yes Bad
2 11.22 83 Yes Yes Good
3 10.06 80 Yes Yes Medium

summary(my.data)

There are no missing data.
Check whether factors are read correctly.

is.factor(my.data$Urban)
[1] TRUE
is.factor(my.data$US)
[1] TRUE
is.factor(my.data$ShelveLoc)
[1] TRUE

Some graphical analyses to evaluate the relationship between the response (Sales) and the covariates.

par(mfrow=c(1,2))
hist(my.data$Sales, prob=TRUE)
boxplot(my.data$Sales, col='grey', ylab='Sales', cex.lab=1.2)


![Histogram Sales Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/f5d99f1a-dd8e-46b1-a99c-c465f70645c9)


plot(my.data$Price, my.data$Sales, cex.lab=1.2, xlab='Price', ylab='Sales')

![Dispersion Plot Sales   Price Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/68de7d6b-8a28-4c9a-ad51-4647d8002933)


It seems there is an inverse relationship.

boxplot(my.data$Sales~my.data$Urban, cex.lab=1.2, xlab='Urban', ylab='Sales',cex.names=1.2)

![Boxplot Sales Urban RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/758544bb-0a15-4d11-b930-9c2b98aaa993)

It seems there are no variations of Sales with respect to Urban, on average.

boxplot(my.data$Sales~my.data$US, cex.lab=1.2, xlab='US', ylab='Sales', cex.names=1.2)

![Boxplot Sales US RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/59abdcca-98ee-4012-b216-d7cd8dd8b20a)


Is there anything interesting?

boxplot(my.data$Sales~my.data$ShelveLoc, cex.lab=1.2, xlab='ShelveLoc', ylab='Sales', cex.names=1.2)


![Boxplot Sales ShelveLoc RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/72cb7de2-b2e9-4a80-9ebf-d0998f8e1a9c)

Is there anything interesting? Dispersion plot according to the levels of Urban

plot(my.data$Price, my.data$Sales, cex.lab=1.2, xlab='Price', ylab='Sales')
points(my.data$Price[my.data$Urban=='Yes'], my.data$Sales[my.data$Urban=='Yes'], col=2)
points(my.data$Price[my.data$Urban=='No'], my.data$Sales[my.data$Urban=='No'], col=3)
legend('bottomleft', col=c('red','green'), pch=c(19,19),
legend=c('Urban=Yes','Urban=No'))

![Dispersion Plot Sales   Price Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/172bf853-6617-4d56-ab96-59da8fccef22)

The partial overlapping of the observations belonging to the two groups suggests that there would not be interactions between the covariates.
Dispersion plot according to the levels of US

plot(my.data$Price, my.data$Sales, cex.lab=1.2, xlab='Price', ylab='Sales')
points(my.data$Price[my.data$US=='Yes'], my.data$Sales[my.data$US=='Yes'], col='red')
points(my.data$Price[my.data$US=='No'], my.data$Sales[my.data$US=='No'], col='green')
legend('bottomleft', col=c('red','green'), pch=c(19,19),
legend=c('US=Yes','US=No'))


![Dispersion plot Sales Price with US factor RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/56d76f9b-44e6-438e-a9f6-b05503c506e6)

How can we interpret the plot?
Dispersion plot according to the levels of ShelveLoc

plot(my.data$Price, my.data$Sales, cex.lab=1.2, xlab='Price', ylab='Sales')
points(my.data$Price[my.data$ShelveLoc=='Bad'],
my.data$Sales[my.data$ShelveLoc=='Bad'], col='red')
points(my.data$Price[my.data$ShelveLoc=='Good'],
my.data$Sales[my.data$ShelveLoc=='Good'], col='green')
points(my.data$Price[my.data$ShelveLoc=='Medium'],
my.data$Sales[my.data$ShelveLoc=='Medium'], col='orange')
legend('bottomleft', col=c('red', 'green', 'orange'), pch=c(19,19, 19),
legend=c('ShelveLoc=Bad', 'ShelveLoc=Good', 'ShelveLoc=Medium'),
bty='n', cex=0.8)

![Dispersion plot Sales Price with ShelveLoc factor RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/d9159358-5f56-4a93-adef-ef371cfe26e5)

How can we interpret the plot? 
Variations of Sales with respect to two factors.

boxplot(my.data$Sales~ my.data$US*my.data$ShelveLoc, las=2, cex.axis=0.7, xlab='', main='Sales vs US and ShelveLoc')


![Boxplot Sales vs US and ShelveLoc RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/cfdd78cb-a3f8-4763-8b05-8d94d1cc1bfe)

boxplot(my.data$Sales~ my.data$Urban*my.data$ShelveLoc, las=2, cex.axis=0.7, xlab='', main='Sales vs Urban and ShelveLoc')


![Boxplot Sales vs Urban and ShelveLoc RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/176506bc-adcd-43d9-9129-8cdb7bba455a)

boxplot(my.data$Sales~ my.data$Urban*my.data$US, las=2, cex.axis=0.7, xlab='', main='Sales vs Urban and US')

![Boxplot Sales vs Urban and US RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/7fbf8e82-fe4c-479b-85c0-da7bbf5c5996)

Interactions seem to be not significant. Why?
Consider a mosaicplot to see the frequencies of![Mosaicplot Urban vs US Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/b3879a32-3957-4245-a925-112c154e81d6)
observations from a couple of factors.

mosaicplot(table(my.data$Urban, my.data$US), main='Urban vs US')

![Mosaicplot Urban vs US Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/41df7905-265d-4cc0-a741-6d9ffff44be4)


mosaicplot(table(my.data$Urban, my.data$ShelveLoc), main='Urban vs ShelveLoc')

![Mosaicplot Urban vs ShelveLoc Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/17e2e3bb-aa91-4823-87e4-54d9b241849a)



mosaicplot(table(my.data$US, my.data$ShelveLoc), main='US vs ShelveLoc')

![Mosaicplot US vs ShelveLoc Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/adea3320-026e-4b30-bcd6-011a9410d0e4)


No relevant variations.
Estimate the multiple linear regression model, for the moment inserting the interactions

model.sales <- lm(Sales~Price + Urban + US + ShelveLoc + Price:ShelveLoc + Price:US +
Price:Urban + ShelveLoc:Urban + ShelveLoc:US + US:Urban, data=my.data)
summary(model.sales)
<br>


How do we interpret the coefficients associated to the qualitative variables?
Try to simplify the model, eliminating some interactions

model.sales2 <- update(model.sales, .~.-Price:US)
summary(model.sales2)

model.sales3 <- update(model.sales2, .~.-Urban:ShelveLoc)
summary(model.sales3)

model.sales4 <- update(model.sales3, .~.-Price:ShelveLoc)
summary(model.sales4)

model.sales5 <- update(model.sales4, .~.-Urban:US)
summary(model.sales5)

model.sales6 <- update(model.sales5, .~.-US:ShelveLoc)
summary(model.sales6)

model.sales7 <- update(model.sales6, .~.-Price:Urban)
summary(model.sales7)

model.sales8 <- update(model.sales7, .~.-Urban)
summary(model.sales8)

anova(model.sales8, model.sales)

par(mfrow=c(2,2))
plot(model.sales8)

![Residual analysis from model sales8 Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/fe341c07-edb5-43df-8411-bb71d6fa2b2e)

confint(model.sales8)



Predictions of sales for a store in US, when the price of the carseat is 115 $ and when
ShelveLoc is Medium:

estimate <- coef(model.sales8)
estimate[1] + estimate[2]*115 + estimate[3] + estimate[5]
(Intercept)
7.732908

How does the prediction change when ShelveLoc is Bad?

estimate[1] + estimate[2]*115 + estimate[3]
(Intercept)
5.839548

Is it useful to insert a polynomial in Price?

summary(update(model.sales8, .~.+I(Price^2)))

No.
Suppose we want to change the baseline level for one qualitative variabile. For example,
we change the baseline level of ShelveLoc from Bad to Good. There are two possibilities

first possibility
new.shelveloc <- my.data$ShelveLoc
contrasts(new.shelveloc) <- contr.treatment(levels(new.shelveloc),
base=which(levels(new.shelveloc) == 'Good'))
second possibility
new.shelveloc2 <- relevel(Carseats$ShelveLoc, ref='Good')

Function contrasts() allows more possibilities to specify contrasts (levels, relationships
among levels), while relevel() only allows to change the reference level. They are
equivalent for our purpose.

model.sales9 <- update(model.sales8, .~. - ShelveLoc + new.shelveloc2)
summary(model.sales9)

Note that the results are coherent with those from model.sales8, with obvious changes
in signs and values of the coefficients associated to the dummies in Shelveloc.
