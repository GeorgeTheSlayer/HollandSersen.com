---
author: Holland
title: Getting Started with the Electrosmith Daisy Seed Part 1
date: 2021-10-07 12:46
description: 
---



## Abstract
The [Electrosmith Daisy Seed][DaisySeed] is a [microprocessor](https://en.wikipedia.org/wiki/Microprocessor) made for [embedded](https://en.wikipedia.org/wiki/Embedded_system) music applications. It allows for the rapid development of devices such as audio effects and synthesizers. 
 
 __This tutorial will go over how to setup your Daisy and create a simple synthesizer using VS Code__

 **PLEASE NOTE:** This tutorial was made for Mac. This means the following:
 - __Return__ is equivalent to __Enter__ on Windows. 
 - __Command (CMD)__ on mac is equivalent to __CTRL__.
 - **Console Commands may be different on Windows.**


## Table Of Contents (For Reference)

- [Part 1: Overview](#part-1-overview)
	- [What is the Electrosmith Daisy?](#what-is-the-electrosmith-daisy)
	- [Prerequisites:](#prerequisites)
- [Part 2: Uploading Example Code](#part-2-uploading-example-code)
	- [Table of contents:](#table-of-contents)
	- [Opening the Folder in VS Code](#opening-the-folder-in-vs-code)
	- [Explaining the Code](#explaining-the-code)
	- [Compiling the Code](#compiling-the-code)
		- [One of Two Results Should Occur:](#one-of-two-results-should-occur)
		- [If Neither of the Outputs Above Appear But This Does](#if-neither-of-the-outputs-above-appear-but-this-does)
		- [If You Don't Get Any of These Then:](#if-you-dont-get-any-of-these-then)
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
	- [Adding Hardware in Code.](#adding-hardware-in-code)
- [References](#references)

# Part 1: Overview
## What is the Electrosmith Daisy?
**The [Electrosmith Daisy][DaisySeed] is an embedded computer made specifically for audio applications.** 

Pros:
- Dedicated Audio inputs and Outputs allows for creation of synthesizers and audio effects right out of the box. 
- Fast processor means no dropouts when preforming live. 
- Plenty of IO allows for projects with many knobs, buttons and screens to be created without another board.  

Cons:
- $30 is a lot for a part.
- No reason to use unless you are using audio in or out.

This product is one of the best solutions for making music related projects, like synthesizers or audio effects.  
**I would not recommend this product for things that have nothing to do with audio.**   
A good alternative would be the [Ardiuno Uno](https://store-usa.arduino.cc/products/arduino-uno-rev3?selectedStore=us) or [Rasberry Pi](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/). 

## Prerequisites:
Since this is for beginners the tutorials won't go into advanced [C++][Cpp] coding or hardware design. However, links for you to explore those topics on your own will be included in the description below.  
This tutorial will not go into any [DSP][DSP] or physics however links will be provided to further knowledge on these subjects.   

For software you will need: 
- [VS Code](https://code.visualstudio.com),
- [The Daisy Tool Chains](https://github.com/electro-smith/DaisyToolchain) 
- [The Daisy Examples Repository](https://github.com/electro-smith/DaisyExamples)
     
For Hardware you will need:
- [Electrosmith Daisy Seed][DaisySeed]
- [One Breadboard](https://www.amazon.com/BB830-Solderless-Plug-BreadBoard-tie-Points/dp/B0040Z4QN8/ref=sr_1_19?dchild=1&keywords=breadboard&qid=1634682261&sr=8-19) (get a nice one, trust me it's worth it)
- [One Micro Usb Cable](https://www.amazon.com/AmazonBasics-Male-Micro-Cable-Black/dp/B0711PVX6Z/ref=sr_1_3?dchild=1&keywords=micro+usb&qid=1634682300&sr=8-3)
- [One Audio Jack](https://www.amazon.com/Honbay-Socket-Stratocaster-Replacement-Electric/dp/B01M0IQ5QI/ref=sr_1_1?crid=L6JVSNGFO20R&dchild=1&keywords=1%2F4+jack&qid=1634682366&sprefix=1%2F4%2Caps%2C174&sr=8-1)
- Two 10k potentiometers
- [One Button](https://www.amazon.com/Cylewet-Momentary-Button-Switch-CYT1078/dp/B0752RMB7Q/ref=sr_1_4?crid=10ONVMUKMJFGL&dchild=1&keywords=button+electronic&qid=1634682399&sprefix=button+elec%2Caps%2C180&sr=8-4) 
- [An Assortment of Wires](https://www.amazon.com/TUOFENG-Wire-Solid-different-colored-spools/dp/B07TX6BX47/ref=sr_1_8?dchild=1&keywords=breadboard+wires&qid=1634682429&sr=8-8). 

# Part 2: Uploading Example Code
## Table of contents:
1. [Opening the Folder in VS Code](#opening-the-folder-in-vs-code)
2. [Explaining the Code](#explaining-the-code)
3. [Compiling the Code](#compiling-the-code)
4. [Uploading Code To the Daisy Seed](#uploading-code-to-the-daisy-seed)
5. [Setup Audio Out](#setup-audio-out) 

## Opening the Folder in VS Code

![Folder](/Img/FolderShot.png)

1. Open VS Code.
2. Click on File -> Open.
3. Find the Daisy Examples Folder on your computer. 
4. Click on the Folder Seed -> Oscillator
5. Open the Folder.

In the Daisy Examples Folder you will see a couple other folders labeled seed, pod, patch and petal. In this tutorial we will be using the daisy seed, so we will be using the examples provided in the seed folder.
However if you are using any of the other Electrosmith platforms then you should go into the corresponding folder for said platform.


## Explaining the Code
So now that we are in the folder, you can now see that the contents of this folder are all open and available to be edited in VS Code. There are multiple files here in this folder the main one we will be concerned about is the Oscilator.cpp file.

**The Oscilator.cpp file defines what our Daisy is doing.**
It is an ordered set of instructions for our Daisy to process when it starts up.
	
For now, all you need to know is that this particular program creates a simple sound (a sine wave to be exact) for us to verify that we have everything up and running.

## Compiling the Code

Now that we have the set of instructions that we want the Daisy to execute we now need to turn it into something that the microcontroller can read. 
This process is called **compiling** and it is how we can turn the code from our human language to something the computer can understand.

Doing this is simple, however, **this is where you can tell whether or not the daisy tool chain is setup correctly on your computer.**
1. Click on the terminal button on the bottom right of VS Code. (This should open up a dedicated terminal for you to type in.) 
2. Then type "make" into the console.
3. Click return to enter the command into the terminal. 

### One of Two Results Should Occur:
[comment]: <> (![Terminal Out](/Img/TerminalMake.png))

```console
Hollands-MacBook-Pro:oscillator hollandsersen$ make
arm-none-eabi-g++  -c -mcpu=cortex-m7 -mthumb -mfpu=fpv5-d16 -mfloat-abi=hard  -DUSE_HAL_DRIVER -DSTM32H750xx -DHSE_VALUE=16000000  -DCORE_CM7 -DSTM32H750IB -DARM_MATH_CM7 -DUSE_FULL_LL_DRIVER -include stm32h7xx.h -I../../libdaisy -I../../libdaisy/src/ -I../../libdaisy/src/sys -I../../libdaisy/src/usbd -I../../libdaisy/Drivers/CMSIS/Include/ -I../../libdaisy/Drivers/CMSIS/DSP/Include -I../../libdaisy/Drivers/CMSIS/Device/ST/STM32H7xx/Include -I../../libdaisy/Drivers/STM32H7xx_HAL_Driver/Inc/ -I../../libdaisy/Middlewares/ST/STM32_USB_Device_Library/Core/Inc -I../../libdaisy/core/ -I../../DaisySP/Source -I../../libdaisy/Middlewares/Third_Party/FatFs/src -O2 -Wall -Wno-missing-attributes -fasm -fdata-sections -ffunction-sections -Wno-stringop-overflow -g -ggdb -MMD -MP -MF"build/oscillator.d" -fno-exceptions -fasm -finline -finline-functions-called-once -fshort-enums -fno-move-loop-invariants -fno-unwind-tables -Wno-register -std=gnu++14 -Wa,-a,-ad,-alms=build/oscillator.lst oscillator.cpp -o build/oscillator.o
arm-none-eabi-g++  build/startup_stm32h750xx.o build/oscillator.o   -mcpu=cortex-m7 -mthumb -mfpu=fpv5-d16 -mfloat-abi=hard --specs=nano.specs --specs=nosys.specs -T../../libdaisy/core/STM32H750IB_flash.lds -L../../libdaisy/build -L ../../DaisySP/build -ldaisy -lc -lm -lnosys -ldaisysp -Wl,-Map=build/oscillator.map,--cref -Wl,--gc-sections -Wl,--print-memory-usage -o build/oscillator.elf
Memory region         Used Size  Region Size  %age Used
           FLASH:       42740 B       128 KB     32.61%
         DTCMRAM:          0 GB       128 KB      0.00%
            SRAM:        5076 B       512 KB      0.97%
          RAM_D2:         16 KB       288 KB      5.56%
          RAM_D3:          0 GB        64 KB      0.00%
         ITCMRAM:          0 GB        64 KB      0.00%
           SDRAM:          0 GB        64 MB      0.00%
       QSPIFLASH:          0 GB         8 MB      0.00%
arm-none-eabi-objcopy -O ihex build/oscillator.elf build/oscillator.hex
arm-none-eabi-objcopy -O binary -S build/oscillator.elf build/oscillator.bin
Hollands-MacBook-Pro:oscillator hollandsersen$ 
```

The Terminal will show the memory usage of the code: 
- This means it compiled correctly and you installed the tool chains right too.

[comment]: <> (![Nothing to be done](/Img/NothingToBeDoneMake.png))

```console
Hollands-MacBook-Pro:oscillator hollandsersen$ make
make: Nothing to be done for `all'.
```

The Terminal say "nothing to be done for all". 
- This means the code has already been compiled. It just needs to be uploaded to the Daisy. 	 
  
### If Neither of the Outputs Above Appear But This Does
[comment]: <> (![Fix the Error](/Img/FixErrorMake.png))

```console
Hollands-MacBook-Pro:oscillator hollandsersen$ make
arm-none-eabi-g++  -c -mcpu=cortex-m7 -mthumb -mfpu=fpv5-d16 -mfloat-abi=hard  -DUSE_HAL_DRIVER -DSTM32H750xx -DHSE_VALUE=16000000  -DCORE_CM7 -DSTM32H750IB -DARM_MATH_CM7 -DUSE_FULL_LL_DRIVER -include stm32h7xx.h -I../../libdaisy -I../../libdaisy/src/ -I../../libdaisy/src/sys -I../../libdaisy/src/usbd -I../../libdaisy/Drivers/CMSIS/Include/ -I../../libdaisy/Drivers/CMSIS/DSP/Include -I../../libdaisy/Drivers/CMSIS/Device/ST/STM32H7xx/Include -I../../libdaisy/Drivers/STM32H7xx_HAL_Driver/Inc/ -I../../libdaisy/Middlewares/ST/STM32_USB_Device_Library/Core/Inc -I../../libdaisy/core/ -I../../DaisySP/Source -I../../libdaisy/Middlewares/Third_Party/FatFs/src -O2 -Wall -Wno-missing-attributes -fasm -fdata-sections -ffunction-sections -Wno-stringop-overflow -g -ggdb -MMD -MP -MF"build/oscillator.d" -fno-exceptions -fasm -finline -finline-functions-called-once -fshort-enums -fno-move-loop-invariants -fno-unwind-tables -Wno-register -std=gnu++14 -Wa,-a,-ad,-alms=build/oscillator.lst oscillator.cpp -o build/oscillator.o
oscillator.cpp: In function 'int main()':
oscillator.cpp:47:15: error: expected '}' at end of input
   47 |     while(1) {}
      |               ^
oscillator.cpp:29:1: note: to match this '{'
   29 | {
      | ^
make: *** [build/oscillator.o] Error 1
Hollands-MacBook-Pro:oscillator hollandsersen$ 
```

This means there is an error somewhere in your code:
1. Fix the line of code that the terminal says is wrong
2. Save it
3. Then compile it again by typing make

### If You Don't Get Any of These Then:
1. Make sure the tool chains are all properly installed. 
	- [This video by Electrosmith shows how to install the toolchains properly.](https://www.youtube.com/watch?v=e4KaBs6qSkU&t=599s) 
	- [The GitHub also has a good tutorial located here.][DaisyWIKI]
2. Check that the Daisy Library is compiled. 
	- [The Electrosmith GitHub describes it here.][DaisyEX]


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

Now we need to get audio from the Daisy. We will do this by creating a simple circuit:
1. Plug the Daisy Seed anywhere on your breadboard
  - Make sure that all pins go into the breadboard fully.
2. Plug the Aground pin into the "-" terminal.
3. Plug the Dground pin into the "-" as well.
  - This will insure the Daisy is grounded with the rest of our circuit. 
4. Next get your audio jack.
5. Identify which terminal is "tip"
6. Connect tip to the "Audio Out 1 Pin" (TODO Add pictures and pin number)
7. Identify which terminal is "Ring"
8. Connect ring to the "-" terminal of the breadboard

Now if you connect the Daisy Via Usb you should hear a simple sine wave coming from the device. 


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
- [Make](https://opensource.com/article/18/8/what-how-makefile)
- [VS Code config files](https://opensource.com/article/18/8/what-how-makefile)

## Top of the File:

```Cpp
#include "daisysp.h"
#include "daisy_seed.h"

using namespace daisysp;
using namespace daisy;

static DaisySeed  seed;
static Oscillator osc;
```

**The top section of your program is usually dedicated to linking the libraries and creating the objects to be used throughout the file.**
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

```Cpp
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
```

Let's go through each of these one by one before editing the file. 

### Seed Object:

```Cpp
	seed.Configure(); 
	seed.Init();
```

- Both functions initialize the hardware.
	- This allows for a default state to be created for the hardware which helps with preventing glitches. 
### Sample Rate:

```Cpp
	float sample_rate;
	sample_rate = seed.AudioSampleRate();
```

- [Sample rate](https://en.wikipedia.org/wiki/Sampling) needs to be initialized for use within objects like the oscillator object. 
	- **Anything that has to do with time in our Daisy Program will need the Sample Rate.** 
### Oscillator Initialization and Default Params:
	
```Cpp
// Initialize 
osc.Init(sample_rate);
		
// Set parameters for oscillator
osc.SetWaveform(osc.WAVE_SIN);
osc.SetFreq(440);
osc.SetAmp(0.5);
```
	
- Creates a default state for the oscillator object while also passing in the sample rate. 
	- Set Waveform sets what type of sound the oscillator will play.
		- Currently the waveform is set to a [Sine Wave][Sine].
	- osc.SetFreq() sets the pitch of the oscillator.
		- The pitch of an oscillator is known as its [frequency][Frequency].
	- Set Amp sets how loud the oscillator is.
		- The loudness of a waveform is known as it's [amplitude][Amplitude].  

**If you do now know what any of these terms mean then please watch the following resources**:
- Waveforms
- Amplitude
- Frequency 
### Start Audio Callback:

```Cpp
    // Start callback
    seed.StartAudio(AudioCallback);
```

- The program then runs the Start Audio function defined in the middle of the file.
- **This function is where the oscillator will be playing, where our audio comes in, and where it comes out making it one of the most important functions in the file.**

### Audio Callback

```Cpp
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
```

- This is where the audio is processed:   
		1. The osc object creates a sine wave.  
		2. The [sine][Sine] wave is played through the **left** speaker.  
		3. The [sine][Sine] wave is played through the **right** speaker.  
Now that we understand the code lets edit the code.

# Editing the Code:
Now we will change the code to fit out needs. We need to change the pitch (known as [frequency][Frequency]) of the synth and the amplitude  

## Change the Frequency:   
 
 First let's change the [frequency][Frequency] of the oscillator.   

```Cpp
// Set parameters for oscillator
osc.SetWaveform(osc.WAVE_SIN);
osc.SetFreq(440);
osc.SetAmp(0.5);
```

Go to the int main(void) function.  

Change:  
```Cpp
osc.SetFreq(440);
```
To 
```Cpp
osc.SetFreq(880);
```

The [frequency][Frequency] has been changed from 440 to 880. Remember that doubling the [frequency][Frequency] will increase the perceived note by one [octave](https://en.wikipedia.org/wiki/Octave). **So this will create a new note one [octave](https://en.wikipedia.org/wiki/Octave) higher than before.** 

## Change the Amplitude
Now let's change the amplitude

Change:
```Cpp
osc.SetAmp(0.5);
```
To:

```Cpp
osc.SetAmp(0.25);
```
		
What this will do is decrease the volume of the waveform to half of what the waveform was before.  

## Uploading the Code (Again)
Finally let's upload the code to the [Daisy Seed][DaisySeed]. 

1. First make sure the file was been saved
2. Then type "make" into the terminal into VS Code
3. Verify that no errors occurred 
4. Connect the [Daisy Seed][DaisySeed] via micro USB
5. Hold the boot button and then click reset to let the daisy accept uploads.
6. Enter __"make program-dfu"__ into your terminal
7. Verify that no errors occurred

Now your Daisy should be playing a pitch one octave higher at half the original volume.

# Part 4: Adding Hardware to the Daisy Seed

Finally let's add a knob and a button so we can control the Daisy. We will set the knob to control the pitch of the Oscillator and a knob to control the Oscillator volume. 

First we will have to create some code to get data from the knob and button. Then we will connect the hardware to the Daisy. 

## Initialize the Knob:
First let's create the code for the Knob. 

1. Create an AdcChannelConfig object called adcConfig.
2. Add the line:

	```Cpp
	adcConfig.InitSingle(seed.GetPin(21));
	```
	* This will initialize pin 21 on the Daisy Seed. 
	* This pin can be any GPIO pin on the Daisy, but we will be using pin 21. 
3. Add the following line:

	```Cpp
	seed.adc.Init(&adcConfig, 1);
	```
	* This will now init the Daisy Seed Hardware with this new configuration. 
4. Add this final line:

	``` Cpp
	seed.adc.Start();
	```
	
- This will start up the Hardware for the Daisy. 

**Your main function should now look like this:**

```Cpp
int main(void)
{
    // initialize seed hardware and oscillator daisysp module
    float sample_rate;
    seed.Configure();
    seed.Init();

	// Set Knob
    AdcChannelConfig adcConfig;
    adcConfig.InitSingle(seed.GetPin(21));
    seed.adc.Init(&adcConfig, 1);

	// Get sample rate and give it to Osc Object
    sample_rate = seed.AudioSampleRate();
    osc.Init(sample_rate);

    // Set parameters for oscillator
    osc.SetWaveform(osc.WAVE_SIN);
    osc.SetFreq(440);
    osc.SetAmp(0.5);

    // start callback
    seed.adc.Start();
    seed.StartAudio(AudioCallback);

    while(1) {}
}
```

## Initialize the Button:
Now let's add in the code for the button. 

1. In your **main** function add this line:

```Cpp
button1.Init(seed.GetPin(28), 1000);
```

**Your main function should now look like this:**

```Cpp
int main(void)
{
    // initialize seed hardware and oscillator daisysp module
    float sample_rate;
    seed.Configure();
    seed.Init();
    
	// Set button to pin 28, to be updated at a 1kHz  samplerate
    button1.Init(seed.GetPin(28), 1000);

	// Set Knob
    AdcChannelConfig adcConfig;
    adcConfig.InitSingle(seed.GetPin(21));
    seed.adc.Init(&adcConfig, 1);

	// Get sample rate and give it to Osc Object
    sample_rate = seed.AudioSampleRate();
    osc.Init(sample_rate);

    // Set parameters for oscillator
    osc.SetWaveform(osc.WAVE_SIN);
    osc.SetFreq(440);
    osc.SetAmp(0.5);

    // start callback
    seed.adc.Start();
    seed.StartAudio(AudioCallback);

    while(1) {}
}
```

## Controlling the Oscillator Object with hardware:
Finally let's configure the code to allow the Osc object to be controlled.

1. For the Knob add these lines to the Audio Callback Function:

	```Cpp
	float knob = seed.adc.GetFloat(0);
	osc.SetFreq(knobOne * 440.0f + 440.0f);
	```
	- This will get the current value of the knob and store it in a variable.
	- The knob will then change the frequency of the Oscillator.  
2. For the Button add these two lines:

	```Cpp
	button1.Debounce();
	osc.SetAmp(button1.Pressed());	
	```
	
	- This will get the value of the button and store it in a variable.
	- The button then change the volume of the Oscillator depending on it's state.  


**The Audio Callback function should look like this:**

```Cpp
    float sig;
    for(size_t i = 0; i < size; i += 2)
    {
        float knob = seed.adc.GetFloat(0);
        osc.SetFreq((knob * 440.0f) + 440.0f);

        button1.Debounce();
        osc.SetAmp(button1.Pressed());

        sig = osc.Process();

        // left out
        out[i] = sig;

        // right out
        out[i + 1] = sig;
        
    }
```

3. Now save the code
4. Upload the code to the Daisy

## Adding the Hardware:
Finally we can add the hardware to the daisy. If you want to know more about the circuits please look at these resources to find out more.

## Knob Schematic:
First let's add the Knob.

1. Wire the first terminal to Ground
2. Wire the middle terminal to pin 21
3. Wire the last terminal to pin 38 

This circuit will take in voltage and will change it depending on the position of the knob. 

## Button Schematic:
Now let's add the button.

1. Wire one terminal to ground
2. Wire the other terminal to Pin 28:


Now the button should work.

# Part 5: References
Congratulations! You just created your first synthesizer!
If you want to learn more about creating synthesizers, coding, and audio effects then here are some useful effects:
- C++
- Synthesizers 
- Audio Effects
- DSP
- Circuits


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



