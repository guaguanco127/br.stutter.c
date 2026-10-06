# Ableton Max for Live device: br.stutter.c.1.2



By Brian Riordan  
[guaguanco127@gmail.com](mailto:guaguanco127@gmail.com)  
[brianriordanmusic@gmail.com](mailto:brianriordanmusic@gmail.com)  
[https://www.brianriordanmusic.com/](https://www.brianriordanmusic.com/) 
  
Repository for br.stutter.c.1.2, with all related files, can be found here: [https://github.com/guaguanco127/br.stutter.c](https://github.com/guaguanco127/br.stutter.c)  
Additional programs can be found here: [https://github.com/guaguanco127/br.max](https://github.com/guaguanco127/br.max)

Versions 1.1 and 1.2 were updated with Max 9. Version 1.0 was created with Max/MSP 8.5.6. 

## Table of Contents 

[What's New in 1.2](#whats-new-in-12)  
[What's New in 1.1](#whats-new-in-11)  
[About](#About)  
[What is a Max for Live Device?](#M4L)  
[How To Install](#Install)  

## What's New in 1.2

- **Stutters on each attack.** Transient Detect now listens for attacks (a sudden jump in level) instead of loudness: every new attack you play re-triggers the stutter once, and a held or sustained note no longer keeps re-triggering.
- **Sensitivity** now sets how sudden a jump has to be to count as an attack (0 = only strong attacks, 1 = softer attacks too). The default of 0.5 suits most playing.
- **Sample-accurate refresh.** The Refresh Point is now checked at audio rate instead of being polled every millisecond, so grains restart exactly at the point, with less load on Max (and Mira).
- Nothing else changed; controls, inlets and presets are the same as 1.1.

## What's New in 1.1

- **Click-free grain switching.** Each new grain is now captured into the silent player and crossfaded in. Before, the new grain was swapped into the player you were hearing and the crossfade cancelled itself, so every re-trigger could click. Latent mode re-triggers can no longer land on top of each other.
- **Backwards playback fixed.** Negative speeds no longer click on every re-trigger, Refresh works correctly in reverse, and the Filter / Amp / Pan shapes still run forward in time (Up rises, Down falls) when the grain plays backwards.
- **No ticks on short grains.** Each grain loop fades in and out over about 5 ms instead of 1% of the loop, so very short grains no longer tick on every repeat.
- **Even-sounding amp envelopes.** Amp Mode shapes now move in decibels (from -40 dB up to full level) and can't click, even on Square or Rand Step.
- **Smoother filter.** Filter sweeps are even in pitch between Freq 1 and Freq 2, and sudden jumps (Square, Rand Step, re-triggers, fast knob moves) are crossfaded so they don't pop. The filter stops using CPU when Filter Type is Off.
- **Constant-power stereo panning.** Panning no longer drops a channel at the edges: both channels are panned and folded together, and pan moves are smoothed so Alt, Rand Step and Rand Start don't click.
- **Shapes follow Refresh.** When Refresh shortens the loop, the Filter / Amp / Pan shapes now play their whole shape across the shortened loop instead of being cut off. Turning the Refresh dial no longer clicks.
- **Loads the way it looks.** All menus and dials are applied as soon as the device loads, so the sound matches the controls without touching anything.
- **Simpler.** Amp Width and Spread were removed (Amp shapes are symmetric, panning always uses the full stereo field).
- **Lower CPU.** About 3-5%.

## <a name="About"></a>About

This is a Max for Live device that is built around the Max/MSP stutter~ object. This contains all features as br.stutter.b but with extras. This effect includes an auto re-triggering feature, auto-detection, adjustment of the phase (starting position) of the grains, and a refresher that restarts the grain when it reaches a certain position within the phase.

For simpler version of this effect, try [br.stutter.a](https://github.com/guaguanco127/br.stutter.a) or [br.stutter.b](https://github.com/guaguanco127/br.stutter.b)
  
**On/Off:** When Stutter is turned on, the signal is interrupted and a history of the signal is repeated based on the grain size. 

**Button:** While the stutter is on, pressing the button acts like a re-trigger, capturing another grain of the live signal that was fed into the stutter at the time, regardless of what the stutter was just playing. There is no feedback option. 

**Speed:** The playback speed of the grains. 1.0 is the default and is normal speed. Negative speeds play the grains backwards. The range is a float from -32.0 and 32.0. 

**Latent Mode:** When "Latent" is on, the stutter waits to record the next grain of sound before switching to the next stutter sound. The latency is equal to the next grain size. This is a valuable feature because it captures what comes next, as opposed to what already has come and gone. Turning the latent mode off captures the previous grain size prior to pressing the re-trigger button. The default is on. 

**Mix Mode:** There are two mix modes, "Gate" and "Insert" with "Gate being the default. "Gate" allows the dry unaffected signal to pass through while the stutter effect is turned off. The dry signal then mutes once the stuter is turnes on. This feature is best in an effects chain. The "Insert" mode does not allow any dry signal to pass through while the stutter effect is turned off. Instead, you only hear the grains play once the effect is turned on. This feature is useful for auxilliary effect return tracks. 

**Auto Mode:** When turned on, it automatically starts to randomly re-trigger the effect. "Auto 1" is compared with "Auto 2" and a random size is chosen between these two parameters. The range is between 100 ms and 2000 ms.

**Auto 1:** The first potential auto mode timings. "Auto 1" is compared with "Auto 2" and a random size is chosen between these two parameters. The range is between 100 ms and 2000 ms. The default is set to 100 ms. 

**Auto 2:** The second potential auto mode timings. "Auto 1" is compared with "Auto 2" and a random size is chosen between these two parameters. The range is between 100 ms and 2000 ms. The default is set to 1000 ms. 

**Transient Detect:** When both "Stutter" and "Detect" are on, the effect and re-trigger will occur automatically based on the transient detection sensitivity settings. Each new attack re-triggers the stutter once; a held or sustained note does not keep re-triggering.   

**Sensitivity:** When both "Stutter" and "Detect" are on, this sets how sudden a jump in level counts as an attack. Between 0. and 1.: 0. is the lowest sensitivity (only strong, sudden attacks), 1. is the most sensitive (softer attacks count too). 0.5 is the default.  

**Refresh Button:** Press this button and the stutter grain will restart from the beginning. 

**Refresh Mode:** Potential modes for automatically restarting the grain from the beginning. When "Off" is selected the "Refresh Point" is reset to 1.0. When "Cascara" is selected, each grain will either play its full duration, or half of its duration. When "Prog" is selected, each grain will either play its full duration, or 66% of its duration. When "Random" is selected, each grain will refresh at a random point in  its duration. All settings except for "Off" reset the "Refresh Point" to 0.0. 

**Refresh Point:** Where in each grain the refresher restarts it, between 0.0 and 1.0. At 1.0 (the default) the grain is never restarted early; at 0.5 it restarts halfway through. The Filter, Amp and Pan shapes stretch to fit the shortened grain.  

**Phase:** Jumps the playing grain to a new position, between 0.0 (the start) and 1.0 (the end). The jump is crossfaded, so it doesn't click. Each refresh restarts the grain from the start.  

**Size:** The size, in milliseconds, of the current grain that is playing. "Size 1" is compared with "Size 2" and a random size is chosen between these two parameters. The range is between 5 ms and 1000 ms. This is only a meter that tells you its size, you cannot adjust it. 

**Size 1:** The first potential size timings. "Size 1" is compared with "Size 2" and a random size is chosen between these two parameters. The range is between 5 ms and 1000 ms. The default is set to 5 ms.

**Size 2:** The second potential size timings. "Size 1" is compared with "Size 2" and a random size is chosen between these two parameters. The range is between 5 ms and 1000 ms. The default is set to 1000 ms.

**Filter Type:** Defines how the grains will be filtered based on the "Filter Shape." "Off" is the default, and the two different filter types are "Lowpass" and "Bandpass" 

**Filter Shape:** The shape of the filter envelope for the duration of each grain. "Sine" is a basic sine ton going up then down. "Up" is a upward phasing sawtooth wave. "Tri" is a triange shape that is the opposite direction of the sine tone. "Down" is the opposite of the "Up" as it is a downward phasing sawtoth wave. "Square" alternates between "Freq 1" and "Freq 2" without phasing in between. "Rand Step" randomly selects a different filter frequency and "Rand Ramp" randomly envelopes to the next filter frequency. The range of the filter is between "Freq 1" and "Freq 2" 

**Freq 1:** The first of the two frequency ranges that dictate the range of the filter shape envelope. Can be set above or below "Freq 2" 

**Freq 2:** The second of the two frequency ranges that dictate the range of the filter shape envelope. Can be set above or below "Freq 1" 

**Ressonance:** The ressonance of the filter. 0. is the default, and the range is between 0.0 and 0.85

**Amp Mode:** Defines how amplitude envelopes will be applied to each grain. Sine moves up then down, up moves from silence up to full amplitude for the duration of the grain, tri moves down then up, down starts at full amplitude then down to silence, rand step is a random amplitude for the duration of each grain, and rand ramp is an envelope that ramps up and down randomly across the duration of the grain.


**Pan Mode:** Defines how the grains will be panned in the stereo field. The different modes are sine tone, right (each grain moves from left to right), triangle, left (each grain moves from right to left), alt (each grain alternates between hard left then right), rand step (each grain starts from a random position) rand ramp (each grain pans in a random direction for its duration before moving differently each time), and rand start (each re-trigger plays from a different random panning position. 




## <a name="M4L"></a>What Is a Max For Live Device?

Max For Live brings the power and flexibility of Max to Ableton Live. Max For Live gives you access to hundreds of exclusive custom plug-ins (Live Devices) as well as the tools to build your own. These can be MIDI and audio effects, audio and video synthesizers, 3D Jitter visuals, as well as tools that interact with the Live application itself, via the Live API.

## <a name="Install"></a>How To Install

1. Make sure you have the Ableton Live Suite installed in your computer. This was tested on version 11. Make sure Ableton is turned off while installing. 

2. For Macintosh:  
Go to your user folder  
Then Music > Ableton > User Library > Presets > Audio Effects  
Copy and paste br.stutter.c.1.2.amxd into that folder

3. For Windows: \Users\[username]\Documents\Ableton\User Library\Presets\Audio Effects\Max Audio Effect     
  
4. Open Ableton Live. On the left-hand side, look for Max for Live > Max Audio Effect and then the name of this device.

5. Either double-click on the device, or drag/drop it onto the track where you wish to use it.

## Version History  

Version 1.2 replaced the transient detector with an attack (onset) detector (one re-trigger per attack) and made the Refresh Point sample-accurate.  
Version 1.1 was updated with Max 9 (see What's New in 1.1).  
Version 1.0 was created with Max/MSP 8.5.6.
