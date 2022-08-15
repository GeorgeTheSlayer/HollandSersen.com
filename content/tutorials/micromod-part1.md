---
author: Holland Mark Sersen
date: 2022-03-07 12:46
description: 
draft: false
---

## Introduction
This post will go into the first steps in my latest project, a synthesizer meant to introduce people into the world of audio, code named "Micro Mod" (for now).

The Micro Mod Synth would allow for people to learn more about audio in a fun and gamified way. By taking the building blocks of modular synthesis and making them less expensive and complex people would be able to explore and interact with sounds in ways they have never been able to before. This would be an opportunity for children K-8 to explore a passion in sound synthesis. 

I want to make a product that would serve as an introduction to the possibilities of audio. My goals for this project are:

1. Keep it accessible and easy
2. Make it fun and engaging
3. Allow exploration for all ages  in computer music or audio in general.


## Ideation

The Micro Mod can be split off into two parts, connectable controllers and the audio processor. 

The Micro Mod allows the user to mix a unique sound. The user gets the chance to combine different elements in different orders to change and create new sounds within the system. Mixing and matching different color and symbol pieces allowing for 16 variations of sound. Within these 16 sound variations, the user can manipulate the sound modulation by twisting one of four play boards. These will be processed through the audio processor playing what the user has created. 

There will be two play modes with a switch on the audio processor. The first would be FreePlay giving the user control over different sound combinations. The seconds would be DJ Mode where the game gives a building series of actions to follow where the user learns how to replicate sounds on the controllers. 

### Controller

The controller would be made out of four separate boards, each connected through RF. The controllers would be responsible for three things:

1.  Identifying the parameter it is changing through RFID
2.  Getting the position of its onboard magnetometer.
3.  Sending the parameter ID and magnetometer position to the audio processor. 

For the controller for now I am using the ESP32. This board works great for prototyping because it already has RF built in with a bunch of supporting libraries as well. In the future however, I would like to use a different microcontroller since the ESP32 consumes too much power and most of the features would not be used.

### Audio Processor

The audio process with have to do three main things:
1. Interpret the ID given by each controller.
2. Interpret the position of each magnetometer and map it to different sound parameters. 
3. Output Audio

For prototyping I am going to use Max MSP, however I will transition the project to an Electrosmith Daisy running the code in C++. 

## Progress Report
- Ideation/Pre Planning Completed 
- Got Max Patch Working with Arduino, RFID and the magnetometer
- Got Wireless connection between Arduino through ESP Now
	- However I think I will be switching to RF Soon

## Next plans
- Finish Max Patch
- Get multiple Boards working with Max patch




