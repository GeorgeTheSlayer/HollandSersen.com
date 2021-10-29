---
title: Daisy Seed Setup Guide
date: 2021-10-07 12:46

---

# Electrosmith Daisy Seed: Getting Started  
By Holland Sersen -
10-07-2021

## Abstract
The [Electrosmith Daisy Seed][DaisySeed] is a microprocessor made for embedded music applications. It allows for the rapid development of devices such as audio effects and synthesizers. 
 
 __This tutorial will go over how to setup your Daisy and create a simple synthesizer using VS Code__


## Outline

- [Electrosmith Daisy Seed: Getting Started](#electrosmith-daisy-seed-getting-started)
	- [Abstract](#abstract)
	- [Outline](#outline)
- [Part 1: Overview](#part-1-overview)
	- [What is the Electrosmith Daisy?](#what-is-the-electrosmith-daisy)
	- [Prerequisites:](#prerequisites)
- [Part 2: Uploading Example Code](#part-2-uploading-example-code)
	- [Table of contents:](#table-of-contents)
	- [Opening the Folder in VS Code](#opening-the-folder-in-vs-code)
	- [Explaining the Code](#explaining-the-code)
	- [Compiling the Code](#compiling-the-code)
		- [One of two results should occur:](#one-of-two-results-should-occur)
		- [If neither of the outputs above appear but this does](#if-neither-of-the-outputs-above-appear-but-this-does)
		- [If you don't get any of these then:](#if-you-dont-get-any-of-these-then)
	- [Uploading Code To the Daisy Seed](#uploading-code-to-the-daisy-seed)
	- [Setup Audio Out](#setup-audio-out)
- [Part 3: Editing the Example Code](#part-3-editing-the-example-code)
	- [Top of the File:](#top-of-the-file)
	- [Main Function:](#main-function)
		- [Seed Object:](#seed-object)
		- [Sample Rate:](#sample-rate)
		- [Oscillator Initialization and Default Params:](#oscillator-initialization-and-default-params)
		- [Start Audio Callback:](#start-audio-callback)
		- [Audio Callback](#audio-callback)
- [Editing the Code:](#editing-the-code)
	- [Change the Frequency:](#change-the-frequency)
	- [Change the Amplitude](#change-the-amplitude)
	- [Uploading the Code (Again)](#uploading-the-code-again)
- [Part 4: Adding Hardware to the Daisy Seed](#part-4-adding-hardware-to-the-daisy-seed)
- [References](#references)

# Part 1: Overview
## What is the Electrosmith Daisy?
**The [Electrosmith Daisy][DaisySeed] is an embedded computer made specifically for audio applications.** 

Pros:
- Dedicated Audio inputs and Outputs allows for creation of synthesizers and audio effects right out of the box. 
- Fast processor means no dropouts when preforming live. 
- Plenty of IO allows for projects with many knobs, buttons and screens to be created without another board.  

Cons:
- Price, however with how much it comes with audio that is debatable.
- No reason to use unless you are using audio in or out.


## Prerequisites:
Since this is for beginners the tutorials won't go into advanced [C++][Cpp] coding or hardware design, however links for you to explore those topics on your own will be included in the description below.  
This also will not go into any [DSP][DSP] or physics however links will be provided to further knowledge on these subjects.   
For software you will need [VS Code](https://code.visualstudio.com), the Daisy Tool Chains installed on your computer, and the Daisy Examples Repository.   
For hardware all you will need is an [Electrosmith Daisy Seed][DaisySeed], a [breadboard](https://www.amazon.com/BB830-Solderless-Plug-BreadBoard-tie-Points/dp/B0040Z4QN8/ref=sr_1_19?dchild=1&keywords=breadboard&qid=1634682261&sr=8-19) (get a nice one, trust me it is worth it), a [micro usb cable](https://www.amazon.com/AmazonBasics-Male-Micro-Cable-Black/dp/B0711PVX6Z/ref=sr_1_3?dchild=1&keywords=micro+usb&qid=1634682300&sr=8-3), an [audio jack](https://www.amazon.com/Honbay-Socket-Stratocaster-Replacement-Electric/dp/B01M0IQ5QI/ref=sr_1_1?crid=L6JVSNGFO20R&dchild=1&keywords=1%2F4+jack&qid=1634682366&sprefix=1%2F4%2Caps%2C174&sr=8-1), two 10k potentiometers, a [button](https://www.amazon.com/Cylewet-Momentary-Button-Switch-CYT1078/dp/B0752RMB7Q/ref=sr_1_4?crid=10ONVMUKMJFGL&dchild=1&keywords=button+electronic&qid=1634682399&sprefix=button+elec%2Caps%2C180&sr=8-4) and some [wires](https://www.amazon.com/TUOFENG-Wire-Solid-different-colored-spools/dp/B07TX6BX47/ref=sr_1_8?dchild=1&keywords=breadboard+wires&qid=1634682429&sr=8-8). 

# Part 2: Uploading Example Code
## Table of contents:
1. [Opening the Folder in VS Code](#opening-the-folder-in-vs-code)
2. [Explaining the Code](#explaining-the-code)
3. [Compiling the Code](#compiling-the-code)
4. [Uploading Code To the Daisy Seed](#uploading-code-to-the-daisy-seed)
5. [Setup Audio Out](#setup-audio-out) 

## Opening the Folder in VS Code

![Folder](/Img/FolderShot.png)

* Open VS Code.
* Click on File -> Open.
* Find the Daisy Examples Folder on your computer. 
* Click on the Folder Seed -> Oscillator
* Open the Folder.

In the Daisy Examples Folder you will see a couple other folders labeled seed, pod, patch and petal. In this tutorial we will be using the daisy seed, so we will be using the examples provided in the seed folder.
However if you are using any of the other Electrosmith platforms then you should go into the corresponding folder for said platform.


## Explaining the Code
So now that we are in the folder, you can now see that the contents of this folder are all open and available to be edited in VS Code. There are multiple files here in this folder the main one we will be concerned about is the Oscilator.cpp file.

**The Oscilator.cpp file defines what our microcontroller is doing.**
It is an ordered set of instructions for our microcontroller to process when it starts up.
	
For now, all you need to know is that this particular program creates a simple sound (a sine wave to be exact) for us to verify that we have everything up and running.

## Compiling the Code

Now that we have the set of instructions that we want the Daisy to execute we now need to turn it into something that the microcontroller can read. 
This process is called **compiling** and it is how we can turn the code from our human language to something the computer can understand.

Doing this is simple, however, **this is where you can tell whether or not the daisy tool chain is setup correctly on your computer.**
- Click on the terminal button on the bottom right of VS Code. (This should open up a dedicated terminal for you to type in.) 
- Then type "make" into the console.
- Click return to enter the command into the terminal. 

### One of two results should occur:
![Terminal Out](/Img/TerminalMake.png)
- The Terminal will show the memory usage of the code: 
	- This means it compiled correctly and you installed the tool chains right too.

![Nothing to be done](/Img/NothingToBeDoneMake.png)
- The Terminal say "nothing to be done for all". 
	- This means the code has already been compiled. It just needs to be uploaded to the Daisy. 	 
  
### If neither of the outputs above appear but this does
![Fix the Error](/Img/FixErrorMake.png)
- This means there is an error somewhere in your code
	- Fix the line of code that the terminal says is wrong
	- Save it
	- Then compile it again but typing make

### If you don't get any of these then:
* Make sure the tool chains are all properly installed. 
	* [This video by Electrosmith shows how to install the toolchains properly.](https://www.youtube.com/watch?v=e4KaBs6qSkU&t=599s) 
	* [The GitHub also has a good tutorial located here.][DaisyWIKI]
* Check that the Daisy Library is compiled. 
	* [The Electrosmith GitHub describes it here.][DaisyEX]


## Uploading Code To the Daisy Seed
Now we need to upload the compiled files to the Daisy.

1. Connect the daisy via micro usb to your computer. 
	- It should light up when you do this. 
2. Hold the boot button and then click reset to let the daisy accept uploads.
	- The reset light should now be brighter when you do this. 
3. Then type in make program-dfu into your terminal. 
	- (No space in program or -dfu)

The terminal should show the erasing of old code and the new code being uploaded into the Daisy.  

**Congrats!! You successfully uploaded code to your Daisy Microcontroller.**  

## Setup Audio Out
TODO **Work on later, concentrate on getting working code.** 

# Part 3: Editing the Example Code
This section will be dedicated to showing what the [C++][Cpp] file is doing and how to go about editing it. This section will go over some of the basics of [Digital Signal Processing][DSP]. However, basic [C++][Cpp] knowledge is required.  

Links to [C++][Cpp] tutorials are provided below:
- [Functions](https://www.youtube.com/watch?v=V9zuox47zr0)
- [Classes](https://www.youtube.com/watch?v=2BP8NhxjrO0)
- [Headers](https://www.youtube.com/watch?v=9RJTQmK0YPI&t=97s)
- [Loops](https://www.youtube.com/watch?v=_1AwR-un4Hk)
- [Floats](https://www.youtube.com/watch?v=QsICXFKs9uo)

The Oscilator.cpp file is where all of our [Digital Signal Processing][DSP] will be done. So this tutorial will focus mainly on this file. 

Links to the other file types provided below:
- Make
- VS Code config files

## Top of the File:
	#include "daisysp.h"
	#include "daisy_seed.h"

	using namespace daisysp;
	using namespace daisy;

	static DaisySeed  seed;
	static Oscillator osc;
**The top section of your program is usually dedicated to linking the libraries and creating the objects to be sued throughout the file.**
- The include statements link the Daisy Library to the program itself.
- Using namespace allows us to not have to type daisy:: or daisysp:: before every function/object in the Daisy Library. 
- Static DaisySeed is an object meant to handle the hardware.
	- This object is what handles all of the hardware for the Daisy so you don't have to configure it yourself. 
	- (The documentation for this object is located on [here][DaisyLIBP] on page 154, however, it is far from helpful for a beginner).
- Static Oscillator is a simple sound generator.
	- The Oscillator object has a variety of different waveforms ([saw](https://en.wikipedia.org/wiki/Sawtooth_wave), [triangle](https://en.wikipedia.org/wiki/Triangle_wave), [square](https://en.wikipedia.org/wiki/Triangle_wave), [sine](https://en.wikipedia.org/wiki/Sine_wave), and [bandlimited](https://www.music.mcgill.ca/~gary/307/week5/bandlimited.html) versions of each of these to be exact).
	- The Oscillator object also has controllable [frequency](https://en.wikipedia.org/wiki/Frequency) and [amplitude](https://en.wikipedia.org/wiki/Amplitude).

## Main Function:

**The Main Function is used primarily for initializing objects and variables to be used in the seed.StartAudio(AudioCallback) function.** 

	int main(void)
	{
		// initialize seed hardware and oscillator daisysp module
		float sample_rate;
		seed.Configure();
		seed.Init();
		sample_rate = seed.AudioSampleRate();
		osc.Init(sample_rate);

		// Set parameters for oscillator
		osc.SetWaveform(osc.WAVE_SIN);
		osc.SetFreq(210);
		osc.SetAmp(0.5);

		// start callback
		seed.StartAudio(AudioCallback);
		
		while(1) {}
	}

Lets go through each of these one by one before editing the file. 

### Seed Object:
	seed.Configure(); 
	seed.Init();
- Both functions initialize the hardware.
	- This allows for a default state to be created for the hardware which helps with preventing glitches. 
### Sample Rate:
	float sample_rate;
	sample_rate = seed.AudioSampleRate();
- [Sample rate](https://en.wikipedia.org/wiki/Sampling) needs to be initialized for use within objects like the oscillator object. 
	- **Anything that has to do with time in our Daisy Program will need the Sample Rate.** 
### Oscillator Initialization and Default Params:
		
	osc.Init(sample_rate);
		 
	// Set parameters for oscillator
    osc.SetWaveform(osc.WAVE_SIN);
    osc.SetFreq(440);
    osc.SetAmp(0.5);
	
- Creates a default state for the oscillator object while also passing in the sample rate. 
	- Set Waveform sets what type of sound the oscillator will play.
		- Currently the waveform is set to a [Sine Wave][Sine].
	- Set Freq sets the pitch of the oscillator.
		- The pitch of an oscillator is known as its [frequency][Frequency].
	- Set Amp sets how loud the oscillator is.
		- The loudness of a waveform is known as it's [amplitude][Amplitude].  

**If you do now know what any of these terms mean then please watch the following reasources**:
- Waveforms
- Amplitude
- Frequency 
### Start Audio Callback:
    // Start callback
    seed.StartAudio(AudioCallback);
- The program then runs the Start Audio function defined in the middle of the file.
- **This function is where the oscillator will be playing, where our audio comes in, and where it comes out making it one of the most important functions in the file.**

### Audio Callback

		static void AudioCallback(AudioHandle::InterleavingInputBuffer  in, AudioHandle::InterleavingOutputBuffer out, size_t, size)             
		{
		    float sig;
		    for(size_t i = 0; i < size; i += 2)
		    {
		        sig = osc.Process();
		
		        // left out
		        out[i] = sig;
		
		        // right out
		        out[i + 1] = sig;
		        
		    }
		}

- This is where the audio is processed:   
		1. The osc object creates a sine wave.  
		2. The [sine][Sine] wave is played through the **left** speaker.  
		3. The [sine][Sine] wave is played through the **right** speaker.  
Now that we understand the code let's edit the code.

# Editing the Code:
Now we will change the code to fit out needs. We need to change the pitch (known as [frequency][Frequency]) of the synth and the amplitude  

## Change the Frequency:   
 
 First let's change the [frequency][Frequency] of the oscillator.   

	// Set parameters for oscillator
	osc.SetWaveform(osc.WAVE_SIN);
	osc.SetFreq(440);
	osc.SetAmp(0.5);

Go to the int main(void) function.  

Change:  

		osc.SetFreq(440);
To 
		
		osc.SetFreq(880);

The [frequency][Frequency] has been changed from 440 to 880. Remember that doubling the [frequency][Frequency] will increase the perceived note by one [octave](https://en.wikipedia.org/wiki/Octave). **So this will create a new note one [octave](https://en.wikipedia.org/wiki/Octave) higher than before.** 

## Change the Amplitude
Now let's change the amplitude

Change:

		osc.SetAmp(0.5);
To:

		osc.SetAmp(0.25);
		
What this will do is decrease the volume of the waveform to half of what the waveform was before.  

## Uploading the Code (Again)
Finally let's upload the code to the [Daisy Seed][DaisySeed]. 

- First make sure the file was been saved
- Then type "make" into the terminal into VS Code
- Verify that no errors occurred 
- Connect the [Daisy Seed][DaisySeed] via micro USB
- Hold the boot button and then click reset to let the daisy accept uploads.
- Enter "make program-dfu" into your terminal
- Verify that no errors occurred

Now your Daisy should be playing a pitch one octave higher at half the original volume.

# Part 4: Adding Hardware to the Daisy Seed
TODO Next week


# References 
[Cpp]: https://en.wikipedia.org/wiki/C%2B%2B
[DSP]: https://en.wikipedia.org/wiki/Digital_signal_processing
[DaisyWIKI]: https://github.com/electro-smith/DaisyWiki/wiki
[DaisyEX]: https://github.com/electro-smith/DaisyExamples
[DaisyLIBP]: https://github.com/electro-smith/libDaisy/blob/master/doc/libdaisy_reference.pdf
[Frequency]: https://en.wikipedia.org/wiki/Frequency
[Amplitude]: https://en.wikipedia.org/wiki/Amplitude
[Sine]: https://en.wikipedia.org/wiki/Sine_wave
[DaisySeed]: https://www.electro-smith.com/daisy/daisy















