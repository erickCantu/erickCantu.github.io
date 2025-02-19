---
title: "Predicting Success in Kickstarter  with Machine Learning" 
categories: 
    - Data_Science
    - Maschine Learning

tags: 
    - eda 
    - data science
    - kickstarter
    - logistic regression
    - decisions trees
    - neuefische
    - xgboost
    - adaboost
    - bootcamp

last_modified_at: 2022-06-30-T14:00:00-01:00
image: /assets/images/posts/kickstarter/ecantu_Design_a_vector_illustration_for_a_website_header_with_t_4b6a29c8-3dba-4f9e-b7fe-7e7e16ea12c4.png

---

Machine learning has revolutionized our ability to predict outcomes by leveraging vast amounts of data to uncover hidden patterns and trends. By continually refining predictive models and adapting to new data, machine learning has not only enhanced the accuracy of predictions but also propelled innovation across industries, ultimately paving the way for a smarter, more efficient future. 

## Machine Learning to Predict Kickstarter Success

As part of the Neuefische data science bootcamp, we learn different Machine Learning algorithms, methods and models. We applied them in our second project. Which I conducted it with my colleague Sue Leen Wong. In our *Machine Leaning* project we analyzed data to predict the success of launching a crowdfunding project in [Kickstarter](https://www.kickstarter.com). 

---

## The Project

#### Introduction

Kickstarter, founded in 2009, is a crowdfunding platform where project creators can raise money from the public, circumventing traditional avenues of investment. It has an all-or-nothing funding model, whereby a project is only funded if it meets its goal amount; otherwise no funds are collected.

A huge variety of factors contribute to the success or failure of a project on Kickstarter. Some of these factors are able to be quantified or categorized, which allows for the construction of a model to attempt to predict whether a project will succeed or not.

The goal of this project is to predict if a Kickstart project will succeed or fail through using Exploratory Data Analysis and supervised Machine Learning models.

More generally, the aim is to help potential project creators as well as potential investors assess what their chances of success on Kickstarter will be.

#### The Stakeholder

Mr. Jacoby Stevens  

- Retired entrepreneur 

- Likes supporting crowdfunding projects 

- Is looking for the next big idea 

- Would like us to predict for him the likelihood of success or  failure 

- Wants to support the projects most likely to succeed

#### Baseline Model

- Projects based in USA are likely to be successful

- Evaluation Metric:
  We train the model based on precision. Precision is the ratio of correctly predicted positives out of all of the results that were predicted positive.

- Score for baseline model:
  Precision = 57.8%, Accuracy = 55.2%

#### Takeaways and Future Work

- Improvement in accuracy from 55.2% to 72.0% over the baseline model with XGBoost.

- Best project categories to invest are:
  
  - Comics, dance or publishing categories
  
  - Projects featured as “staff pick” when launched
  
  - Projects from Hong Kong, Japan or Great Britain

- Worst project categories to invest are:
  
  - Technology 
  
  - Food 

---

## Links

The analysis is available at the [Predicting Kickstarter Project Success with Machine Learning](https://github.com/erickCantu/Predicting_Kickstarter_Project_Success) GitHub repository. At the end of the analysis a presentation was done to the Neuefische team and other trainees. This presentation is available at: [ML to predict Kickstarter success](https://github.com/erickCantu/Predicting_Kickstarter_Project_Success/blob/main/Kickstarter_Project_Staff_Meeting_Presentation.pdf).
