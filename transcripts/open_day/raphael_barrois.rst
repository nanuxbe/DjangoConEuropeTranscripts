=======================================================
Raphaël Barrois: Cyberponies - Django talks to machines
=======================================================

NEW SPEAKER:	 Hello everybody.  So, our final talk on this section, please don't go away for lunch, there will be plenty of food left.  So we're going to have one more talk by Raphael on cyber ponies.  Thank you very much.  {Applause}.

RAPHAEL BARROIS:	  I have one option one is I go very, very fast and everybody will be ready soon or I can try to present things in an able manner which I'll do.  Today we're going to talk about {inaudible} cyberponies, Django and machines.  What do I mean by machines?  Where I work we are entering car sharing system in Paris, Lyon, Bordeaux, soon in {inaudible} ... some are cars so they're good with some systems and units and some are charging points so you get a big {inaudible} ... so devices I'm thinking of, you can think of all devices, you can think of traffic lights or small {inaudible} to know what temperature is so what I'm going to talk about days vices that are full of sensors around them that you can promote {inaudible} in terms of traffic light green ... and local interaction like swiping your card on a point.  And all those 3,000 cars and points with Django and I'm going to explain {inaudible}.

What do we need to do?  First you need to manage {inaudible} - your inventory, what devices I have {inaudible} when did I buy them {inaudible} new devices as they come out of the factory or when they come in.  Hopefully you will have to push from {inaudible} new features, basically because we want to {inaudible}.

Monitor devices.  Sensors, things coming up, record everything that happens, everything, road, or ...

And you want to detect issues, sometimes you'll lose a device, drops off or perhaps the {inaudible} is broken or you want to know about it and you want to be able to tell the officer oops there is a problem you cannot transfer this car it's not available right now.

Actually use the device, {inaudible} on your board, it is there, shiny and you want to interact with it.

So you might want to aggregate information from all your devices and put them to your end-users and you want to be able to convert user request from your web-site from your API, from your internal application to actual {inaudible} the devices.

Inventory ... OK the device will {inaudible} inventory,, once a year when replace port ... but you've got serial number, model, manufacturer, mac addresses, registration number, lots and lots of numbers, versions and information to keep, and it has components and subcomponents, when you have a car, hundreds of items in the car and you want to track everything to know perhaps if one batch is malfunctioning.

So just a model, kiosk, that's my internal reference and it's maybe a new kiosk model ... {inaudible} small kiosks, {inaudible} then you've got your actual {inaudible} you install somewhere ..., it has a model, belongs to a customer, it's somewhere in France.  Basically you want to describe your objects Django will be pretty efficient for describing whereabouts.  Put them in and you already have your whole database.  Just with Django.

So if you want to {inaudible} perfect.  If you want history you can use various libraries for instance I think Django reversion keep track of changes, you can use libraries for recording building nice graphs.  You can build a simple APIs {inaudible} information system can access that data.  Your devices can push inventory database and request for API.

OK a few things Django cannot solve.  How do you registering inventory.  If the board is about to scan all parts all serial numbers and push - {inaudible} provided you have device and a huge {inaudible} ... have to scan them manually, and when you want to push on upgrade you want to push up-grade with Django, perhaps you say with Django I want the device to be updated to that from a version but actual {inaudible} on to the device is going to be something else so yeah you have to do something else.

I'm looking for some very, very important thing when you have lots of devices ... internet... {inaudible}.  Security, you want something that says when I am here - it is the right device but it is giving you serial number, someone trying to fake it and when you send data to your devices you want to make sure it's the right data and it's not been altered and it's basically your proper data and someone is not {inaudible} ... that's a few important things when you will have to rely on other tools via Django for instance useful for your place, lots of tools are coming in recently.  So that's more what it is what Django is, the perfect tool because it's {inaudible} devices, you don't want to run Django on your device.

You want also to monitor devices.  Let's say for instance device crashed OK it crashes so {inaudible} it's not working.  OK.  What happened?  Why?  I need to get the last 5 minutes usage or things like that.  I just push a new {inaudible} to all my cards, are they performing better, worse?  I have to know that.  Actually the devices are same source with the charge points, how do we know whether a car is parked in front of charge point?  We need to get that information to know whether we can {inaudible} the charge point or not.  We don't have eyes on the thing.  Our sensors our monitoring - only way we can know what is happening in the interface.  So yeah be prepared to get a huge amount of monitoring traffic.  Sometimes if you get a message once every 5 minutes but 3,000 devices it means you get 10 updates per se second.  Say you wanted to have one once every 5 seconds want to switch to {inaudible} some sort of system so take that into account when deciding your network and system.  But actually if you just want to spread the load of {inaudible} images, send them to the database no problem, {inaudible} application servers running Django because Django is designed you may put several {inaudible} database so if your database is big enough you can {inaudible} ...

A table {inaudible} around {inaudible} lines right now, we can query it pretty fast, postgres is amazing {inaudible} ... elastic, choices to choose from.

That's what I advise is to get all your requests through Django that may if you want to get for instance information about how do the latest engine perform you can look through {inaudible} recorded, {inaudible} then ... monitoring through {inaudible} through Django ... put that in your report.

A few important things to keep in mind when you are distributing system.  You will lose messages.  At some point they will be full or have to miss messages or some will be broken, you will lose messages.  Some messages will arrive late because while the car was parked in another {inaudible} then it has to send 5 hours of data at once.  Sometimes you'll have some issues because your devices have clocks of their own which aren't synchronised so one says this happened 2 p.m. oh actually it was 2.30 when it happened.  You won't be able to do anything.

So tips.  When send message to database just put {inaudible} that may if you have lost an event well, you'll catch up later on next message.

Send the time since last change for all binary sensors.  I know what happened when it happened and I can fix my data.  And what we found very useful is to keep a last known state cache in the database which means we have one line instead of in?  Device so it's much more manageable and have access to all the current state very, very easy.  Good, reports ...

OK now we've got our inventory and we want to use our devices at this point.  Yeah one problem you have is your users they want information about for instance {inaudible} home.  Sources in their home.  So data to provide a global view of the situation and they have lots of devices to consult that are on.  Mobile phones, tablets, they've got their web-site, so you want to put all that information in an agreement so you use {inaudible} proper {inaudible} for err users where Django helps and you want to send commands to your devices when someone acts on its interface, participant, or when your computer needs to reboot or reset some device.  Well, here it helps with Django because for instance let's say I want to reserve a charge point I want to make sure it has {inaudible} received monitoring message recently and it's not used but can create reservation but keep in my Django database for anything else then I send a manual command, blue, that's the logic to charge point and here use the users, I want a reservation, you do that from Django, check the form and you just code your process, {inaudible} user swiping a card.

Huge changes to solve.  You cannot send request from {inaudible} to devices ... here it is more complex - split brain effect which is what happened last time it received message from device.  Partial view world has changed.  You cannot know what has happened you have to guess and have to design and keep that in mind when designing your apps.

That's all so do you have any questions?  {Applause}.

RUSSELL KEITH-MAGEE:	  Are you running Django on both ends of this on the server, devices or just on the server...

RAPHAEL BARROIS:	  Just on the server.  {Inaudible} on the devices but Django {inaudible}.

NEW SPEAKER:	  How do you send out {inaudible} devices the software permit of it.

RAPHAEL BARROIS:	  For now we're using the {inaudible} packages so {inaudible} should be now using version of that much of our meta package so it starts a new package with all occurrences of all versions.  It's not perfect but it works for?  ? And we're looking at oceans like {inaudible} snappy which is going to have {inaudible} devices.

NEW SPEAKER:	 How you deal with tests like for instance you have a device that sends its state, how do you make sure if you use {inaudible} for instance that the device doesn't change over time that you're using the wrong {inaudible} for instance?

RAPHAEL BARROIS: 	 We are building tests where we are running basically the whole ward on the {inaudible} we basically send fake messages to fake device {inaudible} sends a message to the app and back again and so we can {inaudible} like that and build for complex scenario but it's kind of tricky and so we've had project to design simple ways of running full integration tests.  We don't have to run the actual device code which will send {inaudible} want them check the device runs properly and we use some database working to ensure we don't have {inaudible} for the same thing at the same time.

NEW SPEAKER:	  How do you detect that some sensors are broken?

RAPHAEL BARROIS:	  Broken sensors for instance we detect that a sensor is changing states too fast, for instance when a charge point says hey people have been connecting disconnecting 1,000 times in one day you think it's not physically possible so it's broken.  {Inaudible} at all in the time where it should have because we have a few different {inaudible} for instance got to open the charge point to get access to the cable so never opens while you connect disconnect the cable probably is it's broken {inaudible}.

NEW SPEAKER:	 {Inaudible}.

RAPHAEL BARROIS:	  Well, for our next generation vices using web {inaudible} which allows us to send messages direct {inaudible} registration time for comments we want to send to devices.  {Inaudible} more connected state.  It can work for charge points for the cars. It's going to be slightly harder.  Good.  Contact information and if you have any questions about this or perhaps {inaudible} I'm making and perhaps {inaudible} feel free to ring me any time.  {Applause}.

NEW SPEAKER:	  We're going to break for lunch now.  Be back with the timetable by the time you come back.

(APPLAUSE)

(LUNCH)
