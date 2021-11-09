---
title: Electrosmith Daisy Rant
date: 2021-10-07 12:46
draft: true

---

# My Rant on the Electrosmith Platform
## TL;DR The Product is Great. The Documentation is Bad. 
Without bumbling on for too long before we continue I want you to know that **this section is the main reason why I made this tutorial.** When I first got the seed I was amazed at how easy it was to program, yet baffled by the fact that in the documentation it did not mention how to even wire up an audio output. **It took me close to a week to figure that out and another week just trying to get a led to work.** I spent so much time looking through the documentation and examples just to find something. Mind you this platform was advertised to people like me, people who have never programmed or used a microcontroller like Arduino and yet getting audio at from it was near impossible at the time.  

Now yes, **the documentation for the Daisy has improved**. The tutorials on YouTube on how to install the toolchains are really good at helping people get their feet wet, however they haven't yet addressed a core issue which is "what the code is actually doing". As a user you just have to trust that everything just works, which is great for something like Pure Data or Max, but for C++ this prevents you from making anything that is really your own. In my opinion (and I say this having no idea what happens internally in Electrosmith or their philosophy) I think that the Daisy platform and it libraries should be a good starting place not some end all be all professional suite of software tools.  

**If you are a developer then chances are you already have your own library of DSP modules and if you are a beginner your priority should be on learning how to create your own set of software tools.** I think the Daisy has the unique option of catering to both types of people while concentrating more on the little guy. 

These are my suggestions (however Electrosmith is a small company so who knows if they will implement this):
- Documentation on the DaisySp website that includes hardware
- In Depth documentation on some of the "important" classes (OSC, ADSR, filter, etc) 
- Simple but useful circuits for the Daisy Seed. 
