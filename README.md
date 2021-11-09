# PSO-RayTracing-v1.0
Hi, I spent some time and created a custom Ray Tracing profile profile for PSO Blue Burst. Here's how I did it.

The video demo: https://www.youtube.com/watch?v=5TVXPH093gE (Sorry I'm quiet, I don't know what I'm doing.)

Hello, friend.

Do you remember Phantasy Star Online? I think it was the first online multiplayer game for any console. I'll update this if i hear otherwise.
Anyway, I love PSO. Not loved, love. It's fun, good gameplay loop, fun battle mechanics... and I have to say, in the age of Discord and private servers, amazing.

All that said, I have an RTX 2080 "Super" if that matters. So not top of the line, and not the bottom. I like graphics, but i don't need the best to enjoy things.
My problem with RTX is it's only in very specific games, because it takes time to implement. But when done correctly, see: Metro Exodus... it can add replay value and now your $60 game is worth twice as much enoyjoment.

I found a developer who has shaders that ReShade automatically suggest when you install it. They are the qUNIT batch of shaders.
The thing the shader bundle does is lets people like me tinker with little tiny numbers for hours to product a replicable ReShade configuration file that you can customize further to fit your personal aesthetic.

My goal is to show you a demo, get you excited and then get you going.

Here's whats happening. ReShade Shaders in use:
  *  `DELC_Sharpen@qUINT_sharp.fx`
          ->>>> (Sharpens textures)
  *  `MXAO@qUINT_mxao.fx`
          ->>>> (Adds depth to flat textures by drawing darker outlines)
  *  `Bloom@qUINT_bloom.fx`
          ->>>> (The "magic" light effect where brighter things emit glowing light)
  *  `ADOF@qUINT_dof.fx`
          ->>>> (Depth of field... not enabled for video demo because it's hard to make useful)
  *  `DisplayDepth@DisplayDepth.fx`
          ->>>> (Core utility shader to ReShade. I show how to use this for calibration in the demo video, but it's turned off during gameplay)
  *  `RTGlobalIllumination@qUINT_rtgi.fx `
              ->>>> (THE Ray Tracing shader. More on this below.)

The qUINT ones can be retrieved from https://github.com/martymcmodding/qUINT/tree/master/Shaders if you missed them when you install reshade. The have everything above except:

**RTGI (RTGlobalIllumination)**

You may have noticed all shaders except DisplayDepth are named "qUINT_", including the RTGlobalIllumination (or RTGI) shader.
Right now, this shader is going to set to back $5. One time, or if you want beta updates and other cool shaders from the same dev... here's the Patreon: https://www.patreon.com/mcflypg
I am no relation. But there's a Discord for people playing with using this RTGI shader in all kinds of games and sharing their results.
Strong recommend.

**Special considerations and installation**

1. Have an NVIDIA RTX card. AFAIK this only works on an RTX card.
1a. All of this is info provided as-is and use at your own risk. Not sure what all the risks are, so that's why I said that.
2. Download the modded version of ReShade that disables the network buffer overflow: https://github.com/Not-Smelly-Garbage/Reshade-Unlocked/releases -- It's required if you dont want flickering. And you don't want flickering. Just saving you 5 hours there. I'll include the link if I can remember it, or if someone telle me.
3. Install the modded ReShade to the PSOBB exe directory. Make sure to select the qUNIT ones, the rest is up to you. I tested against Ephinea (private PSO server with a great community) but it should work on any PSOBB version for PC.
4. You will need to drop the Dx8toDx9 dll (it's just called d38.dll from here: https://github.com/crosire/d3d8to9/releases). ReShade needs DirectX 9, and that dll is the API that connects the two. This also hung me up for a bit.
    (4a). Now the hardest part. You need to learn how all these modules work to even get anything to start happening on your screen...
5. Just kidding this is the easy part. Download the PSO-RayTracing-v[X].ini file in this repo and slap that bad boy in the root with online.exe and psobb.exe. You know the spot.

That's it, you should be able to launch ReShade when you start PSOBB and select the "PSO-RayTracing-v[X]" profile and... if you've done everything right and stars align

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
