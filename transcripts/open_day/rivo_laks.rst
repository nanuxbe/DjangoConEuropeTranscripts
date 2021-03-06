=======================================
Rivo Laks: Django and the real-time web
=======================================

So, you have got 20 minutes including questions.  So, Rivo Laks travelled from Estonia, on the real-time web with Django, thank you very much.  (APPLAUSE).

RIVO LAKS:  Thanks, I am Rivo, I come from an Estonian product development agency, we use lots of Django in our products and we try to change the world.  Here I am here to talk about Django and the real-time web and how the two link together.

So Django is ten years old and it is certainly a stable and mature framework but when you think about it and the web has changed so much during the last ten years, in 2005 we didn't have small personal computers in our pockets, mobile web didn't exist, Gmail just came out.  It looks like that, paradox 1.0 was also something new.  So the question is, is Django still relevant with all the change requirements that today's web puts on it?

Or has the pony become the dinosaur?

No I don't think so.  Because, Django is actually really modular and really flexible and you can use it to you can use the parts that help you and will show that you can just add a real-time functionality into your application really easily and keep your application up to date so that it hits today’s needs.

So, a small disclaimer real-time web isn't obviously something that must be used everywhere.  My Blog for example doesn't really need real-time updates but, on the other hand it also has some really good news cases where it makes the UI more flexible and fluid and makes the user experience better which is what matters in the end.

So, probably the easiest way that is you just need to push some updates from the server side into the client side when some data changes.  This is commonly known as the Pub Sub.  It is really easy to do in the sense that there are many external services that provide this functionality for you and it is always good use insisting services or libraries where possible you don't really want to reinvent the wheel, but you want to focus on your application and use whatever building blocks are there.

So some of the services include pusher and pusher is what I am going the show today.  They all work pretty much the same way so it doesn't really matter that much which one you want to pick.

You just basically go the pusher website, sign up for a free account and first thing you do is you need to add some code to your server and it is really easy.  First you create the pusher instance, give it your ID and credentials.  Next you can already start sending messages with the trigger function.  The trigger function has 3 important parameters.  First we have the channel which is kind of like chat channels in the sense that when you send a message to the channel then all the clients which are subscribed to the channel and listening to it will receive this message.  The second in this case show message is the message type itself or the name.  So if we are building a chat we could have a show message we could also have join and leave in the names.  Then we have the actual data that we want to send in this case, the message itself and so, with less than 20 lines of code we already have some way of proactively sending updates into the browser whenever something happens.

The next obviously we have to actually receive those messages on the client side in the browser.  This is almost as easy, again we create the pusher instance then we say that we are interested in a certain channel or the message is sent to that channel and then, event handler which reacts to messages of a certain type in, in this case the show message.

Here, in simple demo we just show the model with the receive message.

I want to show a live demo here, there is one, I will give you the link and you can try it afterwards.

You probably also want to have the other direction you want to send the data from the client or the browser to the server and the easiest way to do that is actually bios requests, so you don't need anything fancy there, when the client or the user types something and wants to show a message you do the usual post request to the Django and then Django can push this message forward to all the clients listening.

So, as you can see, it is really easy to add some real-time functionality into your application, talk about the 20 lines of code would probably take about 5 minutes to integrate it and the external services are good again in the sense that you don't have to have your own infrastructure, you don't have to build the building blocks.  You can instead use existing libraries to build your application and focus on what is important for you.

But, sometimes it is not really enough what the external services provide.  For example, you might want to have faster messages or the full control over the messages that you send.  This is where web sockets come in.  So web sockets sees a protocol standardised in 2011 supported on every modern browser.  What web sockets is give you the connection between the browser and the server and it is very low overhead, it is very fast.  It also supports both text and binary data.  In fact we used this binary web sockets where we used to it to work with street lights.  So it is versatile.

Let's also look at how web sockets can be used and integrated within Django, using asyncio library, we will also be using web sockets package which gives you again the building blocks or primitives that you can use to just focus on sending and receiving the messages instead of implementing the web sockets protocol yourself.

Because the web sockets should run on a separate port from your main application, we are also going the need a custom server process for that.

I am skipping some of the code.  But the important part is this, define a handler that gets called whenever a client connects.  Then you can use the web socket to send and receive messages.

Again, very simple.  You can expand on that to basically create the loop that reads messages from client and then processes them in some way like printing them out to the standard output.

On the client code web socket has pretty good standard API so you don't really need any third party library, you can use ... JRS, but also use simple rapper library, I am using something called sawkit.

When the connection is made, it sends a message to the server and waits for incoming messages and reacts to them.  Again, showing the alert.

So I hope I have managed to show that Django and real-time web can relate really easily., easy to use external services like pusher.  Also simple with websockets.  It is not difficult but often some third party service will also get you off quite well.

There is also demo up at Djangocon.thorgate.eu.  There is code.  We also have a stand at the front, please come and see me if you are interested in more.  I will tweet the location of the slides thank you.  (APPLAUSE).

NEW SPEAKER:  Does anyone have any questions?

FROM THE FLOOR:  Not really a question, more a remark, there is a new ... called web bush and ... (INAUDIBLE) we have made an implementation that is called web push and there is an implementation, ... so if you want to ... you can use it.  Basically, when the clients connect to the server, ... you can post ... web socket.

RIVO LAKS:  Okay thank you, that is really interesting to know.

FROM THE FLOOR:  What sort of things would you recommend if you wanted to have a mobile native type app.

RIVO LAKS:  I think pusher has made ... it depends on your needs, for something pusher might be enough or you can use websockets.

FROM THE FLOOR:  How would you handle anything other than a client ... you could (INAUDIBLE) something like a mobile app, so is it just for websites and browsers?  Or can it lead to anything?

RIVO LAKS:  Use it between any two, in the project we are using it to communicate between server and not browser, but many devices which controls street lamps.  So, street lamps, so yes, it is quite versatile.

FROM THE FLOOR:  Try out ... dragon, which is a library that is made for Django, using websockets.

RIVO LAKS:  I have heard of it, but not tried it yet.

NEW SPEAKER:  Okay, let's thank the speaker again.

(APPLAUSE).
