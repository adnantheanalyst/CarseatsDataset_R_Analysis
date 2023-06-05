# CarseatsDataset_R_Analysis
Dataset Carseats contains the information about 400 carseats. Data are included in package ISLR.<br>
<br>
upload library ISLR
<br>
library(ISLR)
<br>
and the dataset<br>
data(Carseats)<br>
<br>
dimension of the data<br>
dim(Carseats)<br>
[1] 400 11 <br> 

variables <br>
names(Carseats) <br>
[1] "Sales" "CompPrice" "Income" "Advertising" "Population" "Price" <br>
[7] "ShelveLoc" "Age" "Education" "Urban" "US" <br>

Extract the variables of interest, namely, Sales, Price, Urban, US, ShelveLoc.<br>

my.data <- Carseats[, c('Sales', 'Price', 'Urban', 'US', 'ShelveLoc')]<br>
my.data[1:3,]<br>

Sales Price Urban US ShelveLoc<br>
1 9.50 120 Yes Yes Bad <br>
2 11.22 83 Yes Yes Good <br>
3 10.06 80 Yes Yes Medium <br>

summary(my.data)<br>

There are no missing data.<br>
Check whether factors are read correctly.<br>
<br>
is.factor(my.data$Urban)<br>
[1] TRUE<br>
is.factor(my.data$US)<br>
[1] TRUE<br>
is.factor(my.data$ShelveLoc)<br>
[1] TRUE<br>

Some graphical analyses to evaluate the relationship between the response (Sales) and the covariates.<br>

par(mfrow=c(1,2))<br>
hist(my.data$Sales, prob=TRUE)<br>
boxplot(my.data$Sales, col='grey', ylab='Sales', cex.lab=1.2)<br>


![Histogram Sales Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/f5d99f1a-dd8e-46b1-a99c-c465f70645c9)


plot(my.data$Price, my.data$Sales, cex.lab=1.2, xlab='Price', ylab='Sales')<br>

![Dispersion Plot Sales   Price Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/68de7d6b-8a28-4c9a-ad51-4647d8002933)


It seems there is an inverse relationship.<br>

boxplot(my.data$Sales~my.data$Urban, cex.lab=1.2, xlab='Urban', ylab='Sales',cex.names=1.2)<br>

![Boxplot Sales Urban RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/758544bb-0a15-4d11-b930-9c2b98aaa993)

It seems there are no variations of Sales with respect to Urban, on average.<br>

boxplot(my.data$Sales~my.data$US, cex.lab=1.2, xlab='US', ylab='Sales', cex.names=1.2)<br>

![Boxplot Sales US RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/59abdcca-98ee-4012-b216-d7cd8dd8b20a)


Is there anything interesting?<br>

boxplot(my.data$Sales~my.data$ShelveLoc, cex.lab=1.2, xlab='ShelveLoc', ylab='Sales', cex.names=1.2)<br>


![Boxplot Sales ShelveLoc RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/72cb7de2-b2e9-4a80-9ebf-d0998f8e1a9c)

Is there anything interesting? Dispersion plot according to the levels of Urban<br>

plot(my.data$Price, my.data$Sales, cex.lab=1.2, xlab='Price', ylab='Sales')<br>
points(my.data$Price[my.data$Urban=='Yes'], my.data$Sales[my.data$Urban=='Yes'], col=2)<br>
points(my.data$Price[my.data$Urban=='No'], my.data$Sales[my.data$Urban=='No'], col=3)<br>
legend('bottomleft', col=c('red','green'), pch=c(19,19), legend=c('Urban=Yes','Urban=No'))<br>

![Dispersion Plot Sales   Price Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/172bf853-6617-4d56-ab96-59da8fccef22)

The partial overlapping of the observations belonging to the two groups suggests that there would not be interactions between the covariates.<br>
Dispersion plot according to the levels of US<br>

plot(my.data$Price, my.data$Sales, cex.lab=1.2, xlab='Price', ylab='Sales')<br>
points(my.data$Price[my.data$US=='Yes'], my.data$Sales[my.data$US=='Yes'], col='red')<br>
points(my.data$Price[my.data$US=='No'], my.data$Sales[my.data$US=='No'], col='green')<br>
legend('bottomleft', col=c('red','green'), pch=c(19,19), legend=c('US=Yes','US=No'))<br>


![Dispersion plot Sales Price with US factor RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/56d76f9b-44e6-438e-a9f6-b05503c506e6)

How can we interpret the plot?<br>
Dispersion plot according to the levels of ShelveLoc <br>

plot(my.data$Price, my.data$Sales, cex.lab=1.2, xlab='Price', ylab='Sales') <br>
points(my.data$Price[my.data$ShelveLoc=='Bad'], my.data$Sales[my.data$ShelveLoc=='Bad'], col='red')<br>
points(my.data$Price[my.data$ShelveLoc=='Good'], my.data$Sales[my.data$ShelveLoc=='Good'], col='green') <br>
points(my.data$Price[my.data$ShelveLoc=='Medium'], my.data$Sales[my.data$ShelveLoc=='Medium'], col='orange') <br>
legend('bottomleft', col=c('red', 'green', 'orange'), pch=c(19,19, 19), legend=c('ShelveLoc=Bad','ShelveLoc=Good','ShelveLoc=Medium'),bty='n',cex=0.8)<br>

![Dispersion plot Sales Price with ShelveLoc factor RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/d9159358-5f56-4a93-adef-ef371cfe26e5)

How can we interpret the plot? <br>
Variations of Sales with respect to two factors.<br>

boxplot(my.data$Sales~ my.data$US*my.data$ShelveLoc, las=2, cex.axis=0.7, xlab='', main='Sales vs US and ShelveLoc') <br>


![Boxplot Sales vs US and ShelveLoc RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/cfdd78cb-a3f8-4763-8b05-8d94d1cc1bfe)

boxplot(my.data$Sales~ my.data$Urban*my.data$ShelveLoc, las=2, cex.axis=0.7, xlab='', main='Sales vs Urban and ShelveLoc') <br>


![Boxplot Sales vs Urban and ShelveLoc RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/176506bc-adcd-43d9-9129-8cdb7bba455a)

boxplot(my.data$Sales~ my.data$Urban*my.data$US, las=2, cex.axis=0.7, xlab='', main='Sales vs Urban and US') <br>

![Boxplot Sales vs Urban and US RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/7fbf8e82-fe4c-479b-85c0-da7bbf5c5996)

Interactions seem to be not significant. Why? <br>
Consider a mosaicplot to see the frequencies of observations from a couple of factors.<br>

![Mosaicplot Urban vs US Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/b3879a32-3957-4245-a925-112c154e81d6)
<br>

mosaicplot(table(my.data$Urban, my.data$US), main='Urban vs US') <br>

![Mosaicplot Urban vs US Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/41df7905-265d-4cc0-a741-6d9ffff44be4)


mosaicplot(table(my.data$Urban, my.data$ShelveLoc), main='Urban vs ShelveLoc') <br>

![Mosaicplot Urban vs ShelveLoc Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/17e2e3bb-aa91-4823-87e4-54d9b241849a)



mosaicplot(table(my.data$US, my.data$ShelveLoc), main='US vs ShelveLoc') <br>

![Mosaicplot US vs ShelveLoc Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/adea3320-026e-4b30-bcd6-011a9410d0e4)


No relevant variations. <br>
Estimate the multiple linear regression model, for the moment inserting the interactions <br>

model.sales <- lm(Sales~Price + Urban + US + ShelveLoc + Price:ShelveLoc + Price:US + Price:Urban + ShelveLoc:Urban + ShelveLoc:US + US:Urban, data=my.data)<br>
summary(model.sales)<br>
<br>


How do we interpret the coefficients associated to the qualitative variables? <br>
Try to simplify the model, eliminating some interactions <br>

model.sales2 <- update(model.sales, .~.-Price:US) <br>
summary(model.sales2) <br>

model.sales3 <- update(model.sales2, .~.-Urban:ShelveLoc) <br>
summary(model.sales3) <br>

model.sales4 <- update(model.sales3, .~.-Price:ShelveLoc) <br>
summary(model.sales4) <br>

model.sales5 <- update(model.sales4, .~.-Urban:US) <br>
summary(model.sales5) <br>

model.sales6 <- update(model.sales5, .~.-US:ShelveLoc) <br>
summary(model.sales6) <br>

model.sales7 <- update(model.sales6, .~.-Price:Urban) <br>
summary(model.sales7) <br>

model.sales8 <- update(model.sales7, .~.-Urban) <br>
summary(model.sales8) <br>

anova(model.sales8, model.sales) <br>

par(mfrow=c(2,2)) <br>
plot(model.sales8) <br>

![Residual analysis from model sales8 Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/fe341c07-edb5-43df-8411-bb71d6fa2b2e)

confint(model.sales8) <br>



Predictions of sales for a store in US, when the price of the carseat is 115 $ and when <br>
ShelveLoc is Medium: <br>

estimate <- coef(model.sales8) <br>
estimate[1] + estimate[2]*115 + estimate[3] + estimate[5] <br>
(Intercept) <br>
7.732908 <br>

How does the prediction change when ShelveLoc is Bad? <br>

estimate[1] + estimate[2]*115 + estimate[3] <br>
(Intercept) <br>
5.839548 <br>

Is it useful to insert a polynomial in Price? <br>

summary(update(model.sales8, .~.+I(Price^2))) <br>

Suppose we want to change the baseline level for one qualitative variabile. For example, we change the baseline level of ShelveLoc from Bad to Good. There are two possibilities
<br>
first possibility <br>
new.shelveloc <- my.data$ShelveLoc <br>
contrasts(new.shelveloc) <- contr.treatment(levels(new.shelveloc), base=which(levels(new.shelveloc) == 'Good')) <br>
second possibility <br>
new.shelveloc2 <- relevel(Carseats$ShelveLoc, ref='Good') <br>

Function contrasts() allows more possibilities to specify contrasts (levels, relationships among levels), while relevel() only allows to change the reference level. They are equivalent for our purpose.
<br>
model.sales9 <- update(model.sales8, .~. - ShelveLoc + new.shelveloc2) <br>
summary(model.sales9) <br>

Note that the results are coherent with those from model.sales8, with obvious changes in signs and values of the coefficients associated to the dummies in Shelveloc.<br>

