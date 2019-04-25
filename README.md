# Project 3: Mini Challenge #3

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
    - time (date/time the message was posted)
    - location (Which neighborhood the message was posted from)
    - account (user handle of the person who posted the message)
    - message (The message itself)
#### Example:
- time	
  - 4/6/20 0:00
- location
  - Weston
- account	
  - Opportunities2
- message
  - Take advantheeseage of theesehese One, theeserembling sales!


## Our Plan
  1. We will characterize conditions by sentiment within the messages, as well as the location. The resources will be recomended by sentiment (negative is worse, positive is good) and the population density of the area. We will have an internal ranking of districts, and the higher the ranking, the more resources would be needed as there would be more poeple in need.

  2. We will identify the changes in need of resources during the earthquake (normal -> active responders/rescue teams), shortly after (5 hours: repairs, rescue crews), and long after (30 hours: power/electricty). The inflection point will be by time and/or the magnitude of the disaster.

  3. We can compare the freq of messages when there is not a disatster, and during/post the disaster, and when the frequency skews back to normal, and there arent mention of needing additional resources we can deem the disaster over.

  4. We will use a static collection (.csv file), but stream that data into the project by time/location property within the data. We won't host all the data in an external database nor stream the data through RESTful API calls. It won't affect our analysis as we are using a hybrid between both.

## The Map
#### Redirecting resources would also have to take into account the proximity from one neighborhood to another. We would have to determine where the resources would come from to save travel time in the real world
![map](https://github.com/HXDU/Project-3-Mini-Challenge-3/blob/master/pics/map_names.png)

## Team Contributions
### H Du
1/3 of everything
### J. Willgrubs
1/3 of everything
### N Gomez
1/3 of everything
