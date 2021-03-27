---
permalink: /about/
title: "About"
---

Every year, researchers atop the IceCube Observatory in the South Pole take samples of the snow heights in order to fuel their climate-based research projects. The only problem is that the data is sparse as researchers cannot afford to take measurements more than a couple times per year and especially not during the 6 months of the year when it is dark. If only there was a way of accurately predicting the snow height for any given time during the year. With recent advances in data science, new machine learning methods may hold the key to solving this problem. 

Over the course of this project, I test various regression based machine learning models over various height and weather data in an attempt to create a usable snow height predictor model. 

The remainder of this paper is split into 3 phases, each phase describes an attempt at solving the problem - each phase describes, the dataset, the preprocessing methods applied, and the ways in which the models were created and tested. 
  
outline - sequential   
- first is what do we have to work with?
- read in that csv file
- show a graph
- strip out just the necessary bits  

next is, using this data, how can we predict the next snow height?  
- next step is to gather the data used for prediction ie the weather data
- picture of weather txt files
- picture of weather data in dataframe
- potentially picture of weather data graph
- check correlations for anything promising - somewhat random so not too helpful

preprocessing data  
- mistake - adjust wind deg to compass heading N S E W
- fix - adjust wind deg, mag to windx, windy vectors
- attempt - using temp, windx, windy, pressure to guess snow height directly
- mistakes - weather not over some time period, instantaneous weather at time of recording snow height
- model not given previous heights yet expected to predict entire snow accumulation of station up to this point
- solution - from snow heights create delta snow heights
- from delta snow heights create delta snow height/year
- for weather find avg temp, avg windx, avg windy, avg pres over time between two snow height measurements
- now input / output is 
- given two dates
- using avg temp, avg windx, avg windy, avg pres of all hourly weather measurements between those two dates
- predict difference in snow height of one station between those two dates  

running ML models  
- show understandable version
- model.fit( train_x, train_y)
- model.predict( test_y)
- returns y_hat guesses - eg. 0.2, 0.4, 0.5, 0.2, 0.1 meters/year
- picture of graph comparing guesses to actual
- repeat for each ML model
- for random forest show reliance on each x input
- create / compare with baseline models
- cross validation
- explain how models are further split up and tested with data
- explain possible need for order conservation when testing these models
- tested difference between these 2 cross validation testing methods
- mistake - combine all stations and use model to predict across all stations
- doesn't work because same x inputs have many outputs (same weather during same timeframe predicting for different stations that get different differences - in snow height during the same timeframe) (very weird that snow height differences aren't more similar across stations)
- normalizing first
- explain need for normalization
- compare data before/after
- compare with/without order conserved testing  

New Approach - remove weather, predict with time series  
- idea was use the stock prediction method of determining next snow height
- preprocess again
- same thing except without the weather and without the delta snow heights step.
- run models again
- looks very good initially but must compare with persistence baseline
- explain persistence baseline for time series data
- show bias for t-1 in the random forest model
- cross validation comparison again
- repreprocess/ rerun
- make model predict delta snow height/year again but for time series
- avoids recency bias
- test differences in cross validation again
- test if normalization makes a difference again
- show comparison of models bar graph
- show comparison of models with/without time series and with/without normalization
- hyperparameter search
- fine tuning models by searching thoroughly through options for best fit
- test other stations to make sure model is not overfit to a particular station  

New Data  
- last batch of data was somewhat sparse - had 162 stations with 24 data points each but since the - model cannot generalize and must predict input/output for each unique station, the model is left  - with sparse training data (about 16 points)
- also old data was not measured at regular intervals, anywhere from 8 months to a year between - measurements
- new data of snow heights came through to test models, this time 162 station with monthly snow - heights for a duration of 40 months
- the new data, mostly followed the same trends as the first 
- here are the results (show graphs) 
Conclusion  
- some models performed slightly better than baseline (so tiny might be a fluke)
- overall due to sparse data limitations and no way to combine all stations worth of data, left - - with favoring simpler machine learning models to attempt the predictions.
- the snow heights differences between the stations differed widely causing the computer to become very confused 
- even the differences in snow height between measurements of a single station varied tremendously
- so much so that might include time of year input if done again
- if there was lots more data - opens up possibility for new modern neural network approaches - which often work miraculously better and better the more data it is able to use. 
