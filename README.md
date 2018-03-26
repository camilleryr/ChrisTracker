# ChrisTracker
A cross platform ecosystem built around tracking my running habits.
Nashville Software School Capstone
Demoed 3/34/2018

### Overview 

This was me in 2008ish...

and this was me in 2018ish...

Over the course of 2017 I started running a lot, because of that first picture.  In the fall of that same year, I enrolled in NSS, a full time, immersive, software development program - and between that and a full time day job it because far to easy for me to skip a day of running here and there.
Since I wanted to avoid the me that was in that first picture, I wanted to build a platform of applications that would keep me accountable for making the choices needed to be the best version of myself

### [Mobile App : React Native](https://github.com/camilleryr/TrackerMobile)
https://github.com/camilleryr/TrackerMobile


It all starts at a react native mobile app that is used to gather data while I jog.
Once turned on the app will draw my course as a poly line the react native map and collect geolocation information from the EXPO Location API.
Once the app is deactivated, the mass of geolocation objects is pushed to the ChrisTracker Web API

## [Web API : C# / ASP.NET](https://github.com/camilleryr/Tracker)
https://github.com/camilleryr/Tracker

The C# / ASP.NET Web API is responsible for consuming raw geolocation information from the mobile app, interacting with the SQLite database, the unstructured storage hosted on Firebase and delivering that information back to the front end clients

Upon receiving information from mobile application, the API will save a copy of the geolocation array to Firebase and retrieve a reference to its location so it can be called upon whenever needed.
It will then parse the original data into JOCOs and will calculate some static datapoints about the tracked activity including total distance, time, average pace, etc.  Leveraging Entity Framework, this information, including the reference to the firebase storage, is added to the SQLite database hosted on the same server.

## [Admin Web APP : C# / ASP.NET MVC](https://github.com/camilleryr/TrackerWebApp)
https://github.com/camilleryr/TrackerWebApp

While building out the additional clients that I desired, I needed a way to make sure that my api was working and interacting with the database in the ways I expected, so I built out a simple MVC client.  It is hosted on the same server as the API and interacts with the same database, so it is a powerful tool in maintaining the integrity of my data as I migrated application locations (mostly it gave me information about what I screwed up and how to fix it...)
As I build out some of the additional features that I have planned, this will become an integral part in working with, and separating out the data into different categories.

## [Desktop Client : React](https://github.com/camilleryr/tracker-client)
https://github.com/camilleryr/tracker-client

A React desktop client for visualizing the data from the Web API via the SQlite and Firebase databases.

The splash page is leverages a DECK.GL overlay on top of a Mapbox map to simultaneously animate all of the routes I have tracked with the application.  (Can you find where I live?  I get why the strava data leask was such a big deal now!)


Once entering the main site, you are presented with a dashboard that will give you detailed information about an individual tracked run, defaulting to the most recent.


The main panel is another Mapbox animation, this time of the route of a single jog


The lower left compnent is a chart (from the ReCharts library) that tracks speed and altitude over distance.


With this project being based all around accountability - I displayed the calendar as a github style heatmap (as that is what being productive looks like) with the luminosity of each block being tied to the total distance of the tracked activity for that day.  This component also displays the date of the activity currently selected as well as the total distance and average pace.
By selecting any block from the heatmap, the other components will re-render to display the corresponding data from that date.


This chart shows the prevalance of each tier of color on the heatmap




[Check out the live ChrisTracker Desktop Client](http://chrismiller.club/tracker-client/)

## Alexa Skill

All of these pieces allowed me to track my running habits and gave me the ability to visualize the data so that I could stay accountable to it, but I had one more problem that I wanted to solve.
After getting home from a run, I didn't want to jump straight onto my computer or mess with my phone more than necessary to get some information about the activity I just tracked - so I built an Alexa skill to tell me as soon as I walk in the door.

After deactivating the mobile app, I can walk into my house and say "Alexa, ask Chris Tracker about my latest run" and she will respond with "Chris' latest run was on {date} was {distance} miles and took {minutes} minutes and {seconds} seconds"
