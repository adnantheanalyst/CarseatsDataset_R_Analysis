# CarseatsDataset_R_Analysis
Dataset Carseats contains the information about 400 carseats. Data are included in
package ISLR.

## upload library ISLR
library(ISLR)
## and the dataset
data(Carseats)
## dimension of the data
dim(Carseats)
## [1] 400 11
## variables
names(Carseats)
## [1] "Sales" "CompPrice" "Income" "Advertising" "Population" "Price"
## [7] "ShelveLoc" "Age" "Education" "Urban" "US"

Extract the variables of interest, namely, Sales, Price, Urban, US, ShelveLoc.

my.data <- Carseats[, c('Sales', 'Price', 'Urban', 'US', 'ShelveLoc')]
my.data[1:3,]

## Sales Price Urban US ShelveLoc
## 1 9.50 120 Yes Yes Bad
## 2 11.22 83 Yes Yes Good
## 3 10.06 80 Yes Yes Medium

summary(my.data)

## Sales Price Urban US ShelveLoc
## Min. : 0.000 Min. : 24.0 No :118 No :142 Bad : 96
## 1st Qu.: 5.390 1st Qu.:100.0 Yes:282 Yes:258 Good : 85
## Median : 7.490 Median :117.0 Medium:219
## Mean : 7.496 Mean :115.8
## 3rd Qu.: 9.320 3rd Qu.:131.0
## Max. :16.270 Max. :191.0

There are no missing data.
Check whether factors are read correctly.

is.factor(my.data$Urban)
## [1] TRUE
is.factor(my.data$US)
## [1] TRUE
is.factor(my.data$ShelveLoc)
## [1] TRUE

Some graphical analyses to evaluate the relationship between the response (Sales) and
the covariates

par(mfrow=c(1,2))
hist(my.data$Sales, prob=TRUE)
boxplot(my.data$Sales, col='grey', ylab='Sales', cex.lab=1.2)


![Histogram Sales Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/f5d99f1a-dd8e-46b1-a99c-c465f70645c9)

plot(my.data$Price, my.data$Sales, cex.lab=1.2, xlab='Price', ylab='Sales')

![Dispersion Plot Sales   Price Rplot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/68de7d6b-8a28-4c9a-ad51-4647d8002933)

It seems there is an inverse relationship.

boxplot(my.data$Sales~my.data$Urban, cex.lab=1.2, xlab='Urban', ylab='Sales',cex.names=1.2)

cex.names=1.2)![Boxplot Sales Urban RPlot](https://github.com/adnantheanalyst/CarseatsDataset_R_Analysis/assets/16821246/758544bb-0a15-4d11-b930-9c2b98aaa993)

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




