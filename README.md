# PSO-RayTracing
Hi, I spent some time and created a custom ReShade profile using a number of shaders (but not too many...) to SIGNIFICANTLY improve PSO Blue Burst's visuals. Here's how I did it and how you can use it yourself. You don't need any special hardware. If you can run this game, you should be able to add ray tracing to it for $5 and the time it takes to follow this guide. The best part? Just hit Home on your keyboard and you can go tweak everything in the shaders using ReShade. Ping me on Discord if you get stuck or something your feedback has helped me improve this guide. I'm in the Ephinea Discord frequently.

The video demo (1.0 settings -- currently 2.2 and much better): https://www.youtube.com/watch?v=5TVXPH093gE (Sorry I'm quiet, I don't know what I'm doing.) New video later today (11/13/21).

Hello, friend.

Do you remember Phantasy Star Online? I think it was the first online multiplayer game for any console. I'll update this if i hear otherwise.
Anyway, I love PSO. Not loved, love. It's fun, good gameplay loop, fun battle mechanics... and I have to say, in the age of Discord and private servers, amazing.

All that said, I have an RTX 2080 "Super" if that matters. So not top of the line, and not the bottom. I like graphics, but i don't need the best to enjoy things.
My problem with RTX is it's only in very specific games, because it takes time to implement. But when done correctly, see: Metro Exodus... it can add replay value and now your $60 game is worth twice as much enoyjoment.

I found a developer who has shaders that ReShade automatically suggest when you install it. They are the qUNIT batch of shaders.
The thing the shader bundle does is lets people like me tinker with little tiny numbers for hours to product a replicable ReShade configuration file that you can customize further to fit your personal aesthetic.

My goal is to show you a demo, get you excited and then get you going.

Here's whats happening. ReShade Shaders referenced in the ini but unused:

  *  `MXAO@qUINT_mxao.fx`
          ->>>> (Adds depth to flat textures by drawing darker outlines)
  *  `ADOF@qUINT_dof.fx`
          ->>>> (Depth of field... not enabled for video demo because it's hard to make useful)

Utility shader for figuring out depth buffer (not needed unless you are tweaking things):

  *  `DisplayDepth@DisplayDepth.fx`
          ->>>> (Core utility shader to ReShade. I show how to use this for calibration in the demo video, but it's turned off during gameplay)

Shaders in active use:
  *  `DELC_Sharpen@qUINT_sharp.fx`
          ->>>> (Sharpens textures)
  *  `Bloom@qUINT_bloom.fx`
          ->>>> (The "magic" light effect where brighter things emit glowing light)

I have included all the shaders above except the following one here: https://github.com/Luminati-nerd-stuff/PSO-RayTracing-v1.0/blob/main/reshade-shaders.zip

  *  `RTGlobalIllumination@qUINT_rtgi.fx `
              ->>>> (THE Ray Tracing shader. More on this below.)

**RTGI (RTGlobalIllumination)**

You may have noticed all shaders except DisplayDepth are named "qUINT_", including the RTGlobalIllumination (or RGTI) shader. Right now, the RGTI shader is going to set you back $5 one time, or if you want beta updates and other cool shaders from the same dev... here's the Patreon: https://www.patreon.com/mcflypg -> I am no relation. But there's a Discord for people playing with using this RTGI shader in all kinds of games and sharing their results.
Strong recommend.

**SETUP**

1. Download my latest shader pack which includes everything except RTGI from here: https://github.com/Luminati-nerd-stuff/PSO-RayTracing-v1.0/blob/main/reshade-shaders.zip , or go get the shaders from their sources. I didn't write any of them. Don't forget the ray tracing shader (RGTI) requires you go sign up for the dev's Patreon.

2. If you have a file named "d3d9.dll" in the root of your PSOBB folder, you can probably skip this step. If you instead have "d3d8.dll" in there, or the default that comes with Ephinea is dinput8.dll...  Go get the latest DX8to9 dll file named "d3d8.dll" from https://github.com/crosire/d3d8to9/releases and put it in the root of the PSOBB directory, overwriting the default if you're asked. Feel free to back anything up at any time. This file makes PSOBB DX9, which lets reshade work.

3. Download the modded version of ReShade that disables the network buffer overflow: https://github.com/Not-Smelly-Garbage/Reshade-Unlocked/releases. It's required for this game to bypass the reshade network buffer overflow. Install it, targeting online.exe, and using DX9. Don't set up any default shaders is my suggestion, my zip has the ones you need except RGTI.

4. Unpack the shaders and put them in the reshade-shaders directory in the PSOBB folder. If there's no reshade-shaders directory, make sure you installed ReShade (the modded one) in step 3 first. If you did that, just make the directory named reshade-shaders and put the contents of the zip in there. In the Reshade install or edit, you can hit "edit ReShade settings" and make sure:
-> Preset is .\PSO-RayTracing[whatever version is].ini
-> Effect path, Texture path is set as such: [Drive]:\Users\[user]\reshade-shaders\Shaders\ and [Drive]:\Users\[user]\reshade-shaders\Textures
-> Leave the rest unchecked, you can enable fps/clock/performance mode in reshade in the game.

5. Download the PSO-RayTracing-v[X].ini file in this repo and put it in the root with online.exe and psobb.exe.

6. When you load the game ReShade defaults to "Home" to launch the menu. You can pick the ini from the top. You may need to set the global processing parameters so I will save you a lot of headaches. Put this in [General] in the ReShade.ini (not my ini, the default reshade one), OR just read it and type the values in ReShade after clicking the button to edit the global preprocessing settings: PreprocessorDefinitions=RESHADE_DEPTH_LINEARIZATION_FAR_PLANE=5000,RESHADE_DEPTH_INPUT_IS_UPSIDE_DOWN=0,RESHADE_DEPTH_INPUT_IS_REVERSED=0,RESHADE_DEPTH_INPUT_IS_LOGARITHMIC=0

That's it, you should be able to launch ReShade when you start PSOBB and select the "PSO-RayTracing-v[X]" profile. It;s still worth learning how it works, especially if you want to tweak things from this point.

**TROUBLESHOOTING**

Make sure you set the depth buffer in reshade (under the d3d9 tab). You might have to use the DisplayDepth shader to see if its detecting depth as you try the different depth buffers with your monitor resolution to find the right one. It can be a little tricky. Actually it's a lot tricky. Please recheck that you did step 6 above.

**UNKNOWNS!!**

1. I don't know how to fix symbol chats. They are like 100 suns brightness because of their zindex and brightness, but still mostly readable. It's the Bloom shader, but I can't fix it, see me if you have questions. Maybe we can solve it together.

2. I don't know how this will run at different resolutions and all that stuff. I tested this on a RTX 2080 Super, not a fantastic CPU, and I think 16mb of RAM. Solid state drives. You may have to adjust stuff or turn things up or off to fit your tastes.

3. Just adding onto #2, your results may vary (like in general). Not just with with this ridiculous graphics thing youre considering, but in real life too. I just discovered the PSO community, and this version of the DC game, and the shaders kind of all at once. I'm learning!

I'll update as needed.
"Life is Chaos, be kind."


**SPECIAL THANKS**

CashCashish on Ephinea, who turned me onto doing this being possible in the first place.

The devs behind the linked repos above, and the RTGI shader dev. Go sign up and get that shader if you have an RTX card and want to play with games like this.

All the kind folks on Ephinea's discord, and the Patreon dev's discord, and Echelon's posts on Pioneer2.net's forums. All very useful info!!

And now at the end of this v1 3-day whirlwind journey, I just discovered a whole thread about this over here as well and ZabaZu and company: https://www.phantasystaronline.net/forum/index.php?/topic/27191-reshade-for-psobb-optional-screen-space-ray-traced-global-illumination/

I'd like to compare notes and try different settings to really dial in a small handful of fun presets: psychedelic, blurry mode... idk.

**SIDE BY SIDES (V2.2)**

PIONEER 2
- https://imgsli.com/ODEzMDQ
- https://imgsli.com/ODEzMDY
- https://imgsli.com/ODEzMDg
- https://imgsli.com/ODEzMDk
- https://imgsli.com/ODEzMTE
- https://imgsli.com/ODEzMTI
- https://imgsli.com/ODEzMTM
- https://imgsli.com/ODEzMTQ

FOREST
- https://imgsli.com/ODEzMTk

EP4
- https://imgsli.com/ODE0Nzk

**MISC**
1. LSD.ini is a fun weird alternative set of parameters for these shaders with soem wacky effects. You can switch between presets and stuff in ReShade.
2. I made a preset for Episode 3 on the DC through Dolphin emulation... https://imgsli.com/ODE3Mjc
Just grab https://github.com/Luminati-nerd-stuff/PSO-RayTracing/blob/main/PSO3-Dolphin%20-The%20Card%20One.ini and use these globals for ReShade: PreprocessorDefinitions=RESHADE_DEPTH_LINEARIZATION_FAR_PLANE=10,RESHADE_DEPTH_INPUT_IS_UPSIDE_DOWN=0,RESHADE_DEPTH_INPUT_IS_REVERSED=0,RESHADE_DEPTH_INPUT_IS_LOGARITHMIC=0,RESHADE_DEPTH_INPUT_X_SCALE=1,RESHADE_DEPTH_INPUT_Y_SCALE=1.090,RESHADE_DEPTH_INPUT_X_PIXEL_OFFSET=0,RESHADE_DEPTH_INPUT_Y_PIXEL_OFFSET=-5,RESHADE_DEPTH_MULTIPLIER=1
