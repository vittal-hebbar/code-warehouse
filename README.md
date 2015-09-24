# code-warehouse

#: prediction using  using neural net for social science dataset
#-----Section 01-------------------------------------------
# get the data

# set working directory
setwd(dirname(file.choose()))
getwd()

# read in data and examine structure - use file street_crime5.csv
street.crime <- read.csv("Anonymizedstreetcrimedataset.csv", stringsAsFactors = FAstrLSE)
str(street.crime)

----------------------------------------------------------------------
  street.rand <- street.crime[order(runif(50)),]
# remove the first text variable
#street.rand <- street.rand[-1]
street.crime <- street.crime[-1]

street.crime <- street.crime[-10]
street.crime <- street.crime[-8]
street.crime <- street.crime[-11]
street.crime <- street.crime[-9]
str(street.crime)
#-----Section 04-------------------------------------------

# create train and test data

streetcrime.train <- street.crime[2:30000,]
streetcrime.test <- street.crime[30000:42089,]
str(streetcrime.test)
str(streetcrime.train)
round(prop.table(table(streetcrime.train$V_age))*100,0)
round(prop.table(table(streetcrime.train$V_eth))*100,0)
round(prop.table(table(streetcrime.test$Repeat))*100,0)

#-----Section 05-------------------------------------------
# training a model on the data

library(kernlab)
install.packages(kernlab)
strreetcrimemodel <- ksvm(Repeat ~ ., data = streetcrime.test, kernel = "vanilladot")
# vanilladot is a Linear kernel; -- WARNING -- takes a long time

# look at basic information about the model
streetcrimemodel
summary(streetcrimemodel)

#-----Section 06-------------------------------------------
# predictions on testing dataset
streetcrime.pred <- predict(streetcrimemodel, streetcrime.test)
head(streetcrime.pred)
table(streetcrime.pred,streetcrime.test$Repeat)
round(prop.table(table(streetcrime.pred, streetcrime.test$Repeat))*100,1)
write.csv(streetcrime.pred,"mydata.csv")
#-----Section 07-------------------------------------------
# look only at agreement vs. non-agreement
predicit1
# construct a vector of TRUE/FALSE indicating correct/incorrect predictions
agreement <- streetcrime.pred == streetcrime.test$V_age
table(agreement)
round(prop.table(table(agreement))*100,1)

#-----Section 08-----------------
rm(list=ls())
-----------------------------------------------------------------------------------------------------------------------------
prediciton using neural net for street crime for non-anonymous dataset

# code-warehouse

#: prediction using  using neural net for social science dataset
#-----Section 01-------------------------------------------
# get the data

# set working directory
setwd(dirname(file.choose()))
getwd()

# read in data and examine structure - use file street_crime5.csv
street.crime <- read.csv("NonAnonymizedstreetcrimedataset.csv", stringsAsFactors = FAstrLSE)
str(street.crime)

----------------------------------------------------------------------
  street.rand <- street.crime[order(runif(50)),]
# remove the first text variable
#street.rand <- street.rand[-1]
street.crime <- street.crime[-1]

street.crime <- street.crime[-10]
street.crime <- street.crime[-8]
street.crime <- street.crime[-11]
street.crime <- street.crime[-9]
str(street.crime)
#-----Section 04-------------------------------------------

# create train and test data

streetcrime.train <- street.crime[2:30000,]
streetcrime.test <- street.crime[30000:42089,]
str(streetcrime.test)
str(streetcrime.train)
round(prop.table(table(streetcrime.train$V_age))*100,0)
round(prop.table(table(streetcrime.train$V_eth))*100,0)
round(prop.table(table(streetcrime.test$Repeat))*100,0)

#-----Section 05-------------------------------------------
# training a model on the data

library(kernlab)
install.packages(kernlab)
strreetcrimemodel <- ksvm(Repeat ~ ., data = streetcrime.test, kernel = "vanilladot")
# vanilladot is a Linear kernel; -- WARNING -- takes a long time

# look at basic information about the model
streetcrimemodel
summary(streetcrimemodel)

#-----Section 06-------------------------------------------
# predictions on testing dataset
streetcrime.pred <- predict(streetcrimemodel, streetcrime.test)
head(streetcrime.pred)
table(streetcrime.pred,streetcrime.test$Repeat)
round(prop.table(table(streetcrime.pred, streetcrime.test$Repeat))*100,1)
write.csv(streetcrime.pred,"mydata.csv")
#-----Section 07-------------------------------------------
# look only at agreement vs. non-agreement
predicit1
# construct a vector of TRUE/FALSE indicating correct/incorrect predictions
agreement <- streetcrime.pred == streetcrime.test$V_age
table(agreement)
round(prop.table(table(agreement))*100,1)

#-----Section 08-----------------
rm(list=ls())
