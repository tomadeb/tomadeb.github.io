---
title: 'Monitoring room temperature at home'
tags:
  - house
---

My current project is to monitor the temperature of several rooms in my house. I want to be able to visualise the tenperatures in the cellars, bedrooms, kitchen and TV room. 

This idea originates from the "less-than-perfect" performance of our thermostat. I woke up a few times recently to find that the girls' [Gro-egg](https://gro.co.uk/product/gro-egg/) was displaying 14°C. The central-heating had not been triggered by the wireless thermostat located near the front door. After a bit of investigation, it turned out that the radio-frequency signal was not reaching the receiver connected to the boiler in the cellars. Since we didn't have this issue last winter, I suspect that either the devices are degrading or there is some interference from another transmitter. Perhaps the new wireless bridge I setup earlier this year or something our new neighaours have installed. 

Anyway, I had then decided to make it a little project to replace these failing devices by something a little smarter, probably involving a couple of Raspberry Pis. So I divided the project into 2 rather arbitrary phases:

Phase 1:
  - to accurately measure temperature at several locations throughout my house using low-power unintrusive sensors.
  - collate data centrally and display in [cacti](http://www.cacti.net/)

Phase 2:
  - to replace the thermostat and receiver I have now. The new solution will need to be more modern, more programmable and obviously aware of the temperature in all the rooms monitored.
  - investigate feasability of centrally controling indidvidual radiator valves in each monitored room.

I am fully aware that I could most likely get a commercial solution that would fit the bill. But the aim is also to learn a few more technologies along the way. I'm keen to make use of free and open source technologies I have never used before, such as [docker](http://www.docker.com), [mongodb](http://www.mongodb.com), [nodejs](https://nodejs.org) and [IOT](https://en.wikipedia.org/wiki/Internet_of_things) to name but a few.

So I came up with the following proposed architecture
  - temperature sensors built around [ESP8266](https://en.wikipedia.org/wiki/ESP8266) and [DS18b20](https://www.maximintegrated.com/en/products/analog/sensors-and-sensor-interface/DS18B20.html). 
  - Sensors will regularly send temperature data to a web service hosted on the house server.
  - Web service will consist of 2 docker containers: 
     - mongodb to provide easy key/value storage 
     - nodejs to provide web interface which will store the data provided by the sensors into the mongodb
  - Cacti will query the web service to get the latest room temperatures and store it into rra files.
 
I will make my best to document all the steps required to build the above system in this blog.

Thanks for reading.

t
