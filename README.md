# Project 3: Mini Challenge #3: http://project3.noahgomez.com/

## Team Members:
- H. Du
- N. Gomez
- J. Willgrubs



## Summary 
In disasters, people reach out to friends and family to check in and discuss what they see happening around them. The city and its emergency response teams are hoping to gain an understanding of the issues facing the citizenry they can’t get through seismic readings and survey responses. They are looking to you to help them turn social media posts into an information source helping guide them as to where to focus efforts and what the concerns of the populace are.

## The Challenge [(link)](https://vast-challenge.github.io/2019/MC3.html)
The City has been using Y*INT to communicate with its citizens, even post-earthquake. However, City officials needs additional information to determine the best way to allocate emergency resources across all neighborhoods of St. Himark. Your task, using your visual analytics on the community Y*INT data, is to determine the types of problems that are occurring across the St. Himark. Then, advise the City on how to prioritize the distribution of resources. Keep in mind that not all sources on Y*INT are reliable, and that priorities may change over time as the state of neighborhoods also changes.

1. Using visual analytics, characterize conditions across the city and recommend how resources should be allocated at 5 hours and 30 hours after the earthquake. Include evidence from the data to support these recommendations. Consider how to allocate resources such as road crews, sewer repair crews, power, and rescue teams. Limit your response to 1000 words and 12 images.

2. Identify at least 3 times when conditions change in a way that warrants a re-allocation of city resources. What were the conditions before and after the inflection point? What locations were affected? Which resources are involved? Limit your response to 1000 words and 10 images.

3. Take the pulse of the community. How has the earthquake affect life in St. Himark? What is the community experiencing outside the realm of the first two questions? Show decision makers summary information and relevant/characteristic examples. Limit your response to 800 words and 8 images

4. The data for this challenge can be analyzed either as a static collection or as a dynamic stream of data, as it would occur in a real emergency. Describe how you analyzed the data - as a static collection or a stream. How do you think this choice affected your analysis? Limit your response to 200 words and 3 images.

## The Data
  - 41942 Rows
  - 4 Columns
    - time (Date/time the message was posted)
    - location (Which neighborhood the message was posted from)
    - account (User handle of the person who posted the message)
    - message (The message itself)
    
### Example Data Entry
  
| Time  | Location           |Account  | Message |
|:-------------:|:-------------:|:-------------:|:-------------:|
| 4/6/20 0:00      | Weston |Opportunities2 | Take advantheeseage of theesehese One, theeserembling sales!|


## Our Plan  
1. First filter out unreliable messages/accounts and characterize conditions by sentiment and location by analyzing the messages. The resources will be recomended by sentiment (negative is worse, positive is good) and the population density of the area. We will have an internal ranking of districts, and the higher the ranking, the more resources would be needed as there would be more poeple in need. (To distinguish reliable information source and unreliable source: Mannually labeling, then apply a classifier to do the rest. Such as: SVM or Naive Bayes. )

2. We will identify the changes in need of resources during the earthquake (normal -> active responders/rescue teams), shortly after (5 hours: repairs, rescue crews), and long after (30 hours: power/electricty). The inflection point will be by time and/or the magnitude of the disaster.

3. We can compare the freq of messages when there is not a disatster, and during/post the disaster, and when the frequency skews back to normal, and there arent mention of needing additional resources we can deem the disaster over.

4. We will use a static collection (.csv file), but stream that data into the project by time/location property within the data. We won't host all the data in an external database nor stream the data through RESTful API calls. It won't affect our analysis as we are using a hybrid between both.

## Files & Solutions  
### 1.EarthquakeKeyWordCount.csv  
To identify the time when earthquake happens: keyword search('quake','earthquake'). This csv file has the number of matched messages for each hour.    
Given a threshold of 20, we can identify the message peak time is:  
- Apr,6: 2pm-4pm, 7pm-8pm  
- Apr,8: 8am-10am, 1pm-2pm, 7pm-8pm    
- Apr,9: 8am-9am, 3pm-4pm  
### By checking the content, the earthquake happens around 2pm, Apr 6. Or at least the first strike comes at this hour.   
![map](https://github.com/HXDU/Project-3-Mini-Challenge-3/blob/master/pics/earthquake_by_mesg_num.png)  

### 2.SentimentCount.csv & Folder: SentiByHourByLoc  
To visualize the sentimental changes of published messages over time, we cut the data into multiple 1-hr trunk, then calculate the sentimental score for each hour. This file has the number of messages that are catergrized as positive, negative, and neutral for each hour. Each file in the folder represents one neighborhood, the count is also calculated by hour.  
A line graph of the sentiment count of the whole city:
![map](https://github.com/HXDU/Project-3-Mini-Challenge-3/blob/master/pics/SentimentCount.png)

### 3. Resources-related keywords identification & resourcesByHrByLoc
To use LDA topic modeling on all data to identify possible resources or needs. Examples: water, food, repair, school, fire, etc.   
Based on the current resources of the city and LDA topic filtering, resources group and its related keywords:  
Fire: fire, smoke, burn, firefighter.   
Power: gas, electricity, power.  
People: volunteers, animals, pets, traffic.   
Medic: medic, hospital, hurt.   
![map](https://github.com/HXDU/Project-3-Mini-Challenge-3/blob/master/pics/topicEarthquake.png)

We assume that the importance of one resource is porpotional to the number of its keywords being mentioned. Therefore, we calculate the count of each group keywords by hour and by location. One message may mention one or more resources, we do not limit one message to one possible resource only. 

### 4. How static data effects our data analysis
First, response speed. To train a LDA topic modeling takes time, so does cross-check with data. Streaming data will slow down the response time. If we were to use the same method for streaming data, it will be necessary to decide on some critical time stamps.    
Second, the overview. Static data provides a better overview of situations during the whole period and over time.    

## St. Himark Resources
#### Hospitals
- Palace Hills 
- Old Town
- Downtown Himark x2
- Broadview neighborhood 
- Terrapin Springs 
- Southton
#### Emergency Services
- 34 fire stations 
#### WATER and SEWER
Call our Emergency Service department if you need emergency service from the Water Department, including having your water shut off because of a broken pipe, observing a broken fire hydrant, or if your water service is off and you are not sure why.
##### Current Water and Sewer Projects:
•	Old Town – old water supply lines are being replaced throughout the neighborhood. We apologize for any inconvenience for this very necessary repair work.
<br>
•	East Parton – a broken water main is currently being repaired at the intersection of Blair and Quealy.
<br>
•	West Parton – routine maintenance on the sewer lines is ongoing.

#### GAS:
- If you smell gas, leave the area immediately and call our emergency service number
#### Garbage
- Residential collection is weekly. Commercial collection is weekly, but can be provided more frequently
#### POWER
- Primarily supplied by the Always Safe Nuclear Power Plant (72%)
- Solar and wind providing 12% and 16% of the total supply
- Old Town – we are working to modernize the electrical distribution system. Expect power outages lasting 30-60 minutes throughout the week. 
- Southwest – repairs to the substation that supplies Southwest is causing intermittent power outages

## Choropleth Map
#### Redirecting resources would also have to take into account the proximity from one neighborhood to another. We would have to determine where the resources would come from to save travel time in the real world
![map](https://github.com/HXDU/Project-3-Mini-Challenge-3/blob/master/pics/map_names.png)

Thank you to Jie Lie (Github: [Artlands](https://github.com/Artlands)) for allowing us to use the geojson [St.Himark map](https://gist.github.com/JsyTim/4f24941f4725789fe066467333e6346e).

## Team Contributions
### H Du
- Pre-processing: filtering, and how conditions will be characterized,Ranking of districts, population
- Creating the stream of data from .csv files to the web app
### N Gomez 
- Make the readme
- Create resources allocation algorithms, using distance between districs, and determining road crews, sewer repair crews, power, and rescue teams, helping with secondary resource graph
### J. Willgrubs
- UI: Create map outline, district transition functions, secondary resource graph


