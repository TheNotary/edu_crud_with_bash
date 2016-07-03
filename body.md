# Build a CRUD Application with Fucking Bash Scripts
July 5, 2016


#### Presentation Notes and Resources:
  - [slides](slides/index.html)
  - [Dockerized Server Environment](https://github.com/TheNotary/webserver-hackme-edu)
  - [tcpdump cheat sheet](https://sites.google.com/site/jimmyxu101/testing/use-tcpdump-to-monitor-http-traffic)


#### ToC

Rough Notes:
  - 


###### Section 1 - How Does the Web Work
  - Server/ Client Relationship
  - HTTP
  - It's just an exchange of Files!


###### Section 2 - What do web servers do?
  
  

###### Section 3 - Bash CRUD
  - 
  - 


# Section 1 - How Does the Web Work

Section 1 might feel a little basic, but to keep yourself entertained, chime in with extra info whenever you feel like it!  Help navigate the lesson, that would be excelent, and if things get out of hand, I'll just bring us back on track.  


## Server/ Client Relationship

The phrase server/ client relationship comes up all the time in the software world.  And that's exactly how the web works.  

<NOTE>this question is too vague</NOTE>
Can anyone tell me what a clients do?  (what does a client do with a server?...)
  - They request things of another machine, (the server) right

That's great, so can someone tell me what a server does?
  - Sits around and waits for clients to take care of
  
  
What's the most popular site in the world?  Google, right.  So when we "USE" google.com what role does google?  Server or client?  
  - Right it's the server, because it's sitting around waiting for us.  

What's the client?
  - YES, web browsers are clients in this model.  They request resources from servers.  


## HTTP
###### graph of https://example.com/resource (https is circled)

So the most commonly used protocols on the web are HTTP and the secure variant, HTTPS.  

It stands for...

###### Slide of server/ client
Most client/ server interactions on the web begin with a browser-client sending an HTTP request to a web server.  

The interaction ends with the web server sending back an HTTP response.  


###### Slide of request file

These requests and responses are nothing more than strings of text.  
That's why they call it hyper text transfer protocol, it's all just a bunch of text.  


###### Firefox Inspector of request

By far, my favorite way to view request and response files is through firefox.  
I've included a slide of the view, but I may as well demonstrate this live.  


###### Slide of TCP Dump in action

I can use a CLI utility to view packets.  CLI stands for command line interface and just means you can run the program on the terminal.  
`sudo tcpdump -A -s 0 -i lo 'tcp port 80 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)'`

  - `-i lo` tells tcpdump to only listen to my loop back adapter, only showing transactions to and from 127.0.0.1
  - there's a filter section between single quotes that make it so I only see the really interesting packets  


###### Slide of using bash to send a TCP stream

Using this snippet we can actually send a valid http request using echo and bash
```
exec 3<>/dev/tcp/localhost/80
echo -e "GET /cgi-bin/bash_hi HTTP/1.1\r\nHost: 127.0.0.1\r\nConnection: close\r\n\r\n" >&3
cat <&3
```


>> So that's all there's is to it!  The transaction between a server/ client is pretty much just an exchange of files.  



###### ASK!

PLEASE ASK ME ANYTHING!  WHAT ARE YOU CURIOUS ABOUT REGARDING THE WEB!!!!



# Section 2 - What do web servers do?

  - Ports
  - Static File Serving
  - fastcgi,
  - Thin details (good at handing over a web request to a web language, can speak directly with web browsers)
  - Fastcgi details
  - 


## Ports

Do you all know about ports?
What are ports?  How many are there?  (2^16, 65,536 ports)
I like to think of ports as doors.  
Sometimes some kind of service will be waiting behind a door listening for a client to knock and then will perform some action for said client.  

Can somebody shout out some examples of services that listen on ports?  
  - Web Servers (80)
  - Samba (tcp: 139, 445; udp: 137, 138)
  - SSH (22)
  - irc (6667)
  - l4d (27015)


Have a look at this URL.

`https://google.com:80`

If we key that into an address bar, we'll be instructing our web browser client to... 
  - utilize the https protocol, 
  - convert the hostname `google.com` into an IP address like 216.58.192.14, and then 
  - send data through a tcp stream to port 80 of the IP address to google.com


>>  SO we can specify a port in a URL!  That's so cool!
>>  Ports are like doors!


## Static File Serving


###### slide:  http://search.lores.eu/index.html

So let's say I'm a webserver.  
And I'm listening behind port 80.  
And someone requests from me a file, like index.html.  
What do you think I'm going to do?

Yeah, if index.html is an actual html file on my file system, I'll simply send it to the client making the request along with some headers.  


## FastCGI

To me, static files are pretty boring.  In recent years, we've gotten much cooler front end assets.  
CSS is actually nice now, javascript is sweet.  HTML5 has good stuff like corner radiii and canvas.  
But I like server side API calls and persistent storage a lot, you only get that from the backend.  


## rack/ wsgi

###### Slide:  <plain words>  Rack, wsgi

Has anyone heard of these terms, rack, and wsgi?  
Does anyone know what they are?  (specifications)

These are adapters applications, they connect things in the HTTP server world to the programming world.  
Let's think about just rack.  
On one end of rack, it wants to hear web requests from web clients.  
So half of rack is that it's a web server.  
The other half of rack is a function call.  
It's calling an application <GOOGLE ME>.

So when you boot up a rack application, you're booting up a web server.  One that is really to run arbitrary ruby commands in.  


###### Slide:  basic rack app

This is a valid rack app.  Valid rack apps need to expose a 'call' method (which will be called on the reciept of web requests) and it needs to respond with an array containing http 1.1 codes.  


# Section 3 - 


## 






Who
haz
thoughts?
