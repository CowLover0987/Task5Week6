# Task 5 Week 6

* * *

## 1. Introduction

Our task was to create an online service, tool of utility, utilising PythonAnywhere, Render, or Oracle Cloud. You may alternatively choose to do this locally. Your outcome should demonstrate communication with an Unreal project using one or more of the following:

* HTTP request
* Delegates
* JSON
* CSV
* Data Tables
* Data Assets

Having the option to use python, having previous expeirance with both python and flask, I gravitated towards using what I had expierance with. This task helps us undertand using new/other lanuages, data-driven systems and external data via HTTP requests..

* * *

## 2. Implementation

For this project I used PythonAnywhere to do my web hosting and Unreal engine with blueprints, the lanuage I used python with the flash framework for the web hosing. I used copiolet to help me identify the right nodes within unreal for converting the data from the HTTP request. I first signed up for the free account at PythonAnywhere and set up a web app and I put in two amounts of data in JSON; Speed of '120' and Message of 'Hello from PythonAnywhere'.

![Web app with data](https://github.com/CowLover0987/Task5Week6/blob/main/ImgAndVid/Screenshot%202026-03-09%20143934.png)
Figure 1: My web app hosted by PythonAnywhere.

Getting those values, one simly to print to screen and then to cast to the player character and change the max walking speed with the Speed of '120', showing how a characers values can be stored externally to be used in game.

![Blueprint](https://github.com/CowLover0987/Task5Week6/blob/main/ImgAndVid/Screenshot%202026-03-09%20160957.png)
Figure 2: Bluepirnts the HTTP request and casting to the player character.

![printing to the screen](https://github.com/CowLover0987/Task5Week6/blob/main/ImgAndVid/Screenshot%202026-03-09%20144026.png)
Figire 3: The message printed to the screeen from the HTTP request data.

* * *

## 3. Outcome 

The final result of the project is when the game starts the Message is printed to the screen and the player character moves very slowey, at the speed of 120. I used python with flask rather than C/C++ and I also used JSON to store data externally to a project , the data is then retreived from within the unreal project.

**Demonstration video link:**

[[link]](https://github.com/CowLover0987/Task5Week6/blob/main/ImgAndVid/Screen%20Recording%202026-03-09%20144417.mp4)

* * *

## 4. Bibliography

_Easy Flask App Deployment with PythonAnywhere | Beginner’s Step-by-Step Guide_ (2024) Directed by Code with Josh. At: [Easy Flask App Deployment with PythonAnywhere | Beginner&#39;s Step-by-Step Guide - YouTube](https://www.youtube.com/watch?v=Bx_jHawKn5A) (Accessed 09/03/2026).

_Simple HTTP GET request within a Blueprint - Unreal Engine 5 Tutorial_ (2023) Directed by Geert Verhoeff - Tutorials. At: [Simple HTTP GET request within a Blueprint - Unreal Engine 5 Tutorial - YouTube](https://www.youtube.com/watch?v=Ln1Dk2pF2Bg) (Accessed 09/03/2026).

* * *

## 5. AI Usage Declaration

I used Copilet to help with identifying nodes for HTTP requests.

* * *
