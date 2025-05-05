# lapora
title: "Predicting Classe Activity Using Random Forest"
author: "Your Name"
output: html_document
{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
library(caret)
library(randomForest)
library(dplyr)
# Load the data
training <- read.csv("pml-training.csv", na.strings = c("NA", "", "#DIV/0!"))
testing <- read.csv("pml-testing.csv", na.strings = c("NA", "", "#DIV/0!"))
# Remove columns with many missing values
training <- training[, colSums(is.na(training)) == 0]
testing <- testing[, colSums(is.na(testing)) == 0]
# Remove irrelevant columns
training <- training[, -c(1:7)]
testing <- testing[, -c(1:7)]
# Partition data
set.seed(123)
inTrain <- createDataPartition(training$classe, p=0.7, list=FALSE)
trainSet <- training[inTrain,]
valSet <- training[-inTrain,]
ctrl <- trainControl(method = "cv", number = 5)
modelRF <- train(classe ~ ., data = trainSet, method = "rf", trControl = ctrl)
predictions <- predict(modelRF, valSet)
confusionMatrix(predictions, valSet$classe)
finalPredictions <- predict(modelRF, testing)
finalPredictions
##**Langkah 2: Compile HTML File**
1. Buka file `.Rmd` di RStudio.
2. Klik **"Knit"** → pilih **"Knit to HTML"**.
3. Simpan hasilnya (biasanya `predict_classe_project.html`).
##**Langkah 3: Unggah ke GitHub**
1. Buat akun GitHub (jika belum punya).
2. Buat repositori baru bernama misalnya `predict-classe`.
3. Unggah dua file berikut:
   - `predict_classe_project.Rmd`
   - `predict_classe_project.html`
4. Salin tautan GitHub dan serahkan sesuai instruksi tugas.



