# 18x18AZ Setup Overview

18x18AZ typically assists with around a dozen events a year, at different schools/venues in the region, including both the middle school and high school state championship. Our goal therefore was to create as high quality of a setup as possible while focusing on reliability, ease of setup, and ease of transport in two standard vehicles. Many of the items contained in this are likely overkill for a VEX event and cheaper alternatives could likely be found, however after having replaced almost all equipment from our original setup due to reliability or portability issues, our general approach has been to attempt to buy professional or near professional grade equipment whenever possible rather than buying a cheaper alternative only to discover issues later on.

# Equipment

## Cable standards

We have attempted to use ruggedized professional grade cables and connectors rather than consumer grade systems wherever possible.

### Video - SDI
For video transmission over long distances, we use SDI, and have found it to be incredibly reliable. We have tried other long-distance video transmission systems in the past such as HdBaseT and USB over Cat5 and have found them to be unreliable. NDI appears to be gaining wider adoption in professional use, and will likely become the dominant standard in the future, but this has the drawback of requiring a more robust network setup and also appears to require more expensive associated equipment. For conversion between SDI and HDMI we have used Black Magic converters and have found them to be very reliable and at a reasonable price point.

### Audio - XLR
For audio transmission we use XLR. We also have a box of miscellaneous adapter cables to convert that audio signal to 3.5mm/RCA/etc as needed to work with venue audio.

### Power - PowerCon
For power cables we have moved from traditional extension cables to using a PowerCon True1 based system. This has the advantage of being a more robust locking connector, being easily distinguishable from extension cords owned by the venue, and ensuring that only people familiar with the setup are setting up power cables, avoiding possible issues with unsafe amounts of current draw over long runs of cable/excessive daisy chaining, etc. This also makes our cables a much more known quantity since the cables stock used to make the cables was selected specifically for worst-case scenarios for our use case considering load and run length, especially compared with cables on unknown quality provided by the venue. For power to field monitors/our projector, we use PowerCon gray to IEC cables. This also has the advantage of ensuring that we do not have any easily accessible standard outlet plugs that somebody may plug an unknown device into.

### Networking - Ethercon
For Ethernet we use Ethercon connectors. Ethercon is a more robust locking connector for ethernet cables. We made this change due to the retaining clips on our ethernet cables frequently getting destroyed during setup/teardown/transit.

## Primary road case

![road case](https://i.imgur.com/eAGZYfE.png)

To the extent possible, all equipment needed to run an event is contained in a single rack mount road case. The road case contains the following equipment:

### PC
The primary streaming/operation PC. The PC has a mid range Ryzen processor from several years ago along with a very basic graphics card necessary for stream encoding. We have not found any compelling need for a high performance computer for 1080p streaming and the other relatively lightweight tasks the computer is used for.

The one specialized component to note about the streaming PC is the SDI input/output card. We use a DeckLink Quad 2 8 channel card. The card itself is very reliable and the driver supports Linux, although the driver cannot be used with the Flatpak of OBS on Linux which required us to manually build OBS from source in order to use it. However, the overall integration into OBS is very good, one of the best features is the ability to send the program feed from OBS to the card as an SDI output, rather than needing to have the projector be driven by an HDMI output from the graphics card, which can sometimes have issues with windows being dragged onto the projector screen/etc. One of the biggest issues with this card is that it only suports "Level B" SDI input, which means that while our field cameras can send 1080p60 video over SDI, because they send it via Level A, we have to use 1080p30 output instead.

We have the following SDI inputs:
- Field camera x 3
- Mobile camera
- Video playback Pi

### Miscellaneous Pis
We have 3 raspberry pis in our rack
- 1 used for match audio
- 1 used for stream-safe music playback
- 1 used for video clip playback

### Audio
We primarily use a Shure SLXD24D wireless microphone system with 2 microphones

We bought this system to replace our original wireless microphone system due to issues with poor signal quality and frequent audio dropouts. Although this system is a good bit more expensive than some of the cheaper systems available, we have found it to be incredibly reliable, and any issues with sound quality we have experienced appear to be the result of lack of audio mixing skill rather than any issue with the microphone itself.

We also have a wired SM58 microphone that is kept near the mixer in case somebody needs to make an announcement/etc.

Our mixer is a Behringer X Air XR12 mixer

We have found this mixer to have all the capabilities that we need, and it was chosen primarily for its rack mount form factor and the number of XLR inputs. Behringer has good support for multiple operating systems including Linux, and the X Air series appears to have a very full-featured API for controlling their mixers programatically, although we do not currently make use of that feature.

In order to have separate music tracks for the venue (using normal copyrighted music) and for the stream (using stream-safe music by Approaching Nirvana) we use the left and right audio channels on the mixer for the stream audio and the house audio. All channels except for the music are played on both the left and right channels, the two music input tracks are sent into two separate channel inputs which are linked together as a "stereo" signal. This allows us to adjust the music levels for both the stream and venue audio at the same time with the same slider, and keep the two audio channels almost completely identical except for the music tracks.

Sony MDR 7506 headphones are used for audio mixing, and we have found them to be very good for hearing details in the audio.

### Networking
- Unifi dream machine pro
- Ubiquti Standard 24 PoE switch

Ubiquiti produces are used across our setup, we also have a Ubiquiti access point and flex mini switches used in our setup. The Ubiquti/Unifi ecosystem was chosen for its unified networking control panel across all network devices. Cheaper options could certainly be used, but this has allowed us greater flexibility and has made it faster to diagnose and address network-related issues at events.

### Power and connectivity
Power is provided by a single PowerCon input to a power strip that powers all equipment in the box.

We have patch panels on the front and back of the case for ethernet to the fields/SDI inputs/network connections/etc.

## Field setup

### Field Road Cases
The equipment required for each field is kept in a small road case. Each case includes a raspberry pi, a flex mini ethernet switch, and the main controller portion of the legacy field control system. Ethernet cables are run from marked ethernet jacks in the road case to the two driver station control boards. An HDMI and gray PowerCon jack are present to provide video signal/power to field monitors. There are three external Ethercon jacks on the road case to allow daisy chaining of network between multiple fields. Power in is provided by a True1 connector, and a passthrough power out is also present to allow power to be daisy chained between multiple field boxes.

![field boxes](https://i.imgur.com/go55ySd.png)

### Field Cameras

Each field has an AViPAS AV-1280 PTZ SDI camera. We have found them to be very reliable, and the video quality is decent, but we have had issues with the autofocus. The API, while poorly documented, is very useful for controlling the cameras from software.

## Miscellaneous

### Mobile Cameras

We had originally used an Android app on a smartphone for our mobile camera for opening ceremonies/alliance selection/etc. This produced mostly workable results, but our setup now makes use of a Sony A7iii based camera setup owned by one of our members. It consists of an A7iii camera, a camera rig mostly made out of compoonents from SmallRig, and a Teradek Bolt 6 HDMI transmitter, with the HDMI converted to SDI by a Blackmagic converter at the receiver end. This is obviously complete overkil for a VEX event, and is only used because no organization funds were actually used to purchase any of it.

## Projector

To convert the SDI video signal sent from the streaming PC to the HDMI used by the projector, as well as to power the projector, we have a small True1/SDI -> PowerCon Gray/HDMI converter box that we place next to the projector.

# Organizational system

## Cable reels

All of our long cables with the exception of power cables are kept spooled on cable spools.

![reel](https://i.imgur.com/GGXqQjJ.png)

[The reels we use](https://www.amazon.com/Woods-82870-Snap-Together-Holds-150-Foot/dp/B001KA4P7I/ref=sr_1_14?crid=DN8442PFAY5L&dib=eyJ2IjoiMSJ9.bdjSNiPU-GvVsW2l5HHKl7v5tPm2g0S-Ng-1Qx2deDHge-_SnB74ZZq8RWz9_1iii-thWgT3EDSkvcXr7gaBGLg6G4XbGGFxsia3BwJGPjnaKoQNq1_h6EipJUs-t2rYquIQvWv9oc8ig-Sq4pZeq0iBPybwDg4R2FaTlszG9gV1_NWFGyxj2WM9DEXRhadyJgIabZAk-bU8Vr3foneeWddlkjplZ9aHE165Jzf1GaM.vwB-hiqb_bHSkQwkYWe3dtCasvdm0tPyX96EoxI-5uQ&dib_tag=se&keywords=cable+spool&qid=1714668631&sprefix=cable+spool%2Caps%2C163&sr=8-14)

This means that we can unspool just the amount that is required for a cable run and no more. This has proven to be much easier to keep organize than relying on spooling cables by hand using tecniques such as the over under method, as volunteers with no experience can easily wind a cable around a reel.

## Organizational boxes

Much of our small equipment is kept in a series of labelled small plastic bins. We have a bin for each field, a bin for our miscellaneous audio/video cables, a bin for small useful backup equipment, etc.
Larger compoonents, especially our long extension cables, are kept in milk creates.

One of the most important things we have added is a large clearly marked first aid kit, which is kept in a prominent location in the mission control area where it can be easily found. It's almost inevitable that somebody will end up cutting themselves on something at some point in a season, a first aid kit should be available and easy to find.

## Bundled cables

For small cables associated with a piece of equipment, the relevant cables have been zip tied together/put in a cable sleeve to form a single cable. For example, our printer's power/USB cables, the projector's power/HDMI cable, and the HDMI/USB/power cable bundle that runs from our computer to the monitors. This makes setup/teardown much easier as the cables are already grouped together, and helps ensure that only the cables required are kept in the box, as it becomes very clearly what each cable is for, as oposed to having a collection of say power cables.

# Software

In order to more effectively operate tournaments, we have developed a custom software suite called Event Orchestrator. Event Orchestrator (EO) replaced Tournament Manager for handling of field control, match queueing, inspection and checkin, and all stream/audience displays in the venue, as well as providing additional features to better integrate with our setup. Critically, at least until the midseason rules update requiring TM for field control, our system was in full compliance with both the VEX rules and the TM EULA, as we never reverse engineered any component of Tournament Manager, and to the extent our system interacted with Tournament Manager it did so through the standard TM web interface. Additionally, TM was still responsible for match generation/ranking/interacting with the RE backend/etc.

## Match scheduling/queueing logic

![overall](https://i.imgur.com/nR4PQzJ.png)
*Overall UI*

One of the major pieces of work done for EO was to reimagine the way qualification matches are handled. TM treats the match schedule as a list of matches in a specific order on predetermined fields, and has no concept of matches either queued next on a field, or matches that have been played but are still being on the field being scored. In our scheduling system, matches are grouped as follows

- Contest - a match or group of matches (in the case of, say, Bo3) with a winner (or a tie, as is possible in qual matches)
- Match - tied to a scored result, made up of one or more sittings
- Sitting - an instance that a match has been played/is scheduled to be played. In the case of a match replay, a sitting is completed but the match is not completed, as a replay of the match (i.e a new sitting) is scheduled

The result of all of this is that, if match 12 is being played on Field 2 and the goal on Field 2 breaks which warrants a replay, the EO operator simply needs to press a button that says "replay match" and "Match 12 Replay" will now show up in the match schedule to be played just before lunch, and it will be assigned to be played on whatever field comes after the field used by the last match before lunch.

There is also the concept of an "On Field Match" and an "On Deck Match" for each field. This operates with a similar amount of flexibility to the way elims matches are placed on fields in elims in TM, but by default the system will automatically place matches on the fields that they were originally scheduled to be played on. However, if there's say an issue with a field and repairing it is taking a while, the EO operator can move matches around to avoid matches being played on the broken field as it's being repaired, and at all points the audience displays/field monitors/etc will show the matches as configured in EO.

Additionally, matches are not automatically removed from the field once the match is played, instead they remain on the field until the sitting is resolved, either with a score, or by marking the match for a replay. This means that the queueing display that queuers see will show the field as "Match 5 - Scoring" until the match is actually scored, at which point they know they can send the next team onto the field because it's done being scored.

![queueing display](https://i.imgur.com/qiZHSdn.png)
*Queueing Display*

Another useful concept is the idea of the "Active Match" and the "Next Match". The active match is the current match being displayed on the audience display, if any. The next match is whatever match is scheduled to be played after this match. However, while by default the system will automatically populate the active match and next match by going through match by match, the operator can easily change things around as needed. The purpose of this is to ensure that the referees have only one button, which either says "start auto", "start driver", "queue next match," or is disabled. They can always trust that they can press that button and things will continue to work. This is especially useful if, say, they need to skip a match on a field and then come back to it. The EO operator just needs to make sure that the right match is marked as "Next Match" and things will work smoothly for everybody at the event.

## Skills fields

Tournament Manager operates on the idea of field sets with a shared field timer. This is why you can only run a single skills match on the competition fields at a time. There is also the problem where the skills referee can accidentally start a match on a competition field. Our system does not rely on a shared timer for the entire field set, instead timers are set on the fields individually. This means that we can run skills matches on all competition fields at the same time. Additionally, competition fields cannot be controlled by the skills control interface unless they have been explicitly set to allow skills runs, e.g. during lunch.

Another advantage of our timer system is that timeouts don't use the field timer, so you don't need to "queue" a timeout on a field, which removes the actual match on the field. Instead you just hit the clearly marked timeout button to call a timeout.

## Inspection/checkin

Another major area of improvement concerns checkin and inspection. EO has a custom checkin and inspection menu, as well as custom displays for this information. The inspection data is automatically updated as the inspector checks boxes off, so once the first box is checked on the inspection sheet, the team gets moved to "In Progress", and once the last item is checked off the team is moved to "Complete", there is no risk of the inspector forgetting to hit save. Additionally, the inspection display automatically hides all completed boxes (although this can be toggled so they're visislbe again), making it easier to spot which inspection points have not been checked yet on a team with partial inspection.

An additional state has been added to checkin called "confirmed no show." If it is confirmed that a team will not be attending the event, the team can be marked as a no show, and they will no longer show up on the inspection summary rollups/in the checkin list/etc. This makes it easier to identify which teams you still need to determine the status of, without having to keep track of which teams you know are just not showing up.

![team list](https://i.imgur.com/XaNhLQj.png)
*Team List*

The team list provides a useful filtering tool to filter teams to show just the not checked in teams/just the teams that have not passed inspection/etc. Additionally, we have a custom website accessible on the internet where we upload inspection data to, meaning that volunteers can simply go to a website on their phone to see, in real time, what teams still need to get inspected, rather than relying on a piece of paper and a clipboard and running back and forth to the team list.

![filter](https://i.imgur.com/L1cG6aR.png)
*Team Filter*

## Inegrated OBS and PTZ camera controls

The software has built in controls for OBS and the PTZ cameras. The software can be configured with scene names in OBS and the IP addresses of the PTZ cameras to synchronize tournament operations, OBS scene switching, and PTZ control. In the most basic example, each field is linked to a specific OBS scene and a specific PTZ preset. When a match is about to be the active match, it will automatically set the OBS preview scene to that field's scene, and call the PTZ camera preset for that field. Then, when the referee hits the queue match button, it will call a scene transition. Only once the scene transition has been completed and the field is being shown on the stream can the referee press the button to start the match. After the match, the scene is automatically transitioned to the results display. Only after the scene has transitioned to the results display can the referee hit the button to queue the next match. This all ensures that OBS is always showing the right view and that matches aren't being started before they're being shown.

![display control](https://i.imgur.com/D1kooKe.png)
*display control*

A more compicated example comes in the case of, say, the award ceremony. For awards we use the following script

- Show presenter
- Presenter: "Our next award is the innovate award"
- Trigger the overlay to show innovate award
- Presenter "the innovate award... the innovate award is presented to..."
- Cut to shot of audience with the PTZ camera
- "Team 123A, example team"
- Trigger the overlay to show the name of the winner
- Wait for the camera operator to get a shot of the award winners coming down, switch to them
- Wait for the award winners to be in view of the PTZ camera, switch back to it
- Wait for the award winners to get the award, remove the award overlay

This is unworklable with a small team if you need to control the cameras, control OBS, and control the TM overlays in different windows. Instead we we have the same display with a series of named presets so we can simply click the "audience shot" button when we need to get the audience shot ready, making everything much easier to manage

## Aesthetic improvements

Aesthetics are ultimately highly subjective, but great care was put into the design of the UI elements

![in match](https://i.imgur.com/b0n0d0b.png)

![results](https://i.imgur.com/9KZ7aOb.png)

![bracket](https://i.imgur.com/HXghoOD.png)

## Ease of use

Our system is just a series of webpages, meaning that there's no app to install. If it can run a web browser, it can work as a display or as a user interface.
