---
layout: "post"
title: "first day at gameloft"
date: 2021-05-10 17:10:36 -0400
categories: jekyll work
permalink: "/:title"
---

As I write this, it is 5:13 PM EST. I just finished my last shift here at Gameloft for the week!

It was a really fun time. I remember the first day I was stressed out of my mind because of how hard it was to start things. I had issues with my hardware (that I can confidently say were out of my control), so I actually had to run back twice in one day to get all the parts I needed - a non-glossy monitor, and a wifi adapter.

After that though, I started reading up on documentation, got to meet the team, and ended up merging my first ticket into the palantir workspace. Let's start.

Gameloft is based in Paris. That's where HQ is located. They have locations in Slovakia, Montreal, Toronto, Brisbane, Ukraine, Spain, and more, and they all have different tasks. Australia's part does small games requested by specific companies, Gameloft Montreal works on Dungeon Hunter and Modern Combat, Ukraine on Spider-Man, etc. We can make games pre-loaded on carriers, which is probably not a thing anymore, and most of our revenue comes from iOS and Android devices. We are moving our initiatives now to Xbox, Switch and PC, which is super exciting!

Let's go over what Gameloft has in it's tech team. On the other side, to start there's the **game admin**, who are a one stop shop for game teams. **CRM** (Customer Relational Management) manages live events in games, like ads, promotions, events themselves, etc. They give access to different services, silos, etc. Now, starting with **ISOPS**: ISOPS was created two years ago, and is an information security platform for online services. We make up all of ISOPS - the **WOA** (World Online Admin, who are responsible for tools, different fish ports, the like), the **WOP** (us), as well as GNS and OGI teams (I'll get into these very soon). There's the online infrastructure, composed of the **GNS** (who provides everything needed for internal teams (ex. switching everyone to VPN when covid hit, mattermost (our own company Slack) and outlook accounts) and **OGI** teams, that create the tools we need as the online service providers. (They also provide the infrastructure for our services at Gameloft, for game teams (ex. hosting game servers), managing machines, resources on machines, machines dedicated to each server, ... etc.) **We are the Federation (or WOP)** - a group of 16 developers that maintain all microservices for our games. We write APIs. The tools team uses these backend APIs to create tools for us, and the game team use our APIs to interact with the online aspects of games. We are essentially the core of everything online games, working with services like matchmaking (Anubis service), chat (Osiris), game saves, leaderboard services, etc. We have a production environment that runs in real time, which we look at to consult our "clients" - the game devs, and have operations where we investigate the code all teams write and raise tickets (concerns) on resources that could be used better or not used at all, things like that (they fix possible and outstanding issues). We "release" alpha versions every monday, betas every Wednesday or Thursdays, and I **believe** gold on Fridays.

There's our team too. The Federation itself used to be two teams, and was created by a person named Benni way back in the day. We have Edmund - who is the team go-to, alongside Olivier. We have Gurprit who's leading everything new we implement, testing technologies that Gameloft could use, etc. We're moving to have 3 teamleads, who developers go to to consult their unique solutions be it the case they have any. (There's a note here about how Legacy is everything that's already live in game teams - not sure what this is but I can confirm it next week). The Federation has qualities that we like to pursue, which Anna, our manager, described to me as "quality and automation" - just like any good developer, we request advice from our client (or our "stakeholder") **before starting**. We also have the word "done", which can be very taboo if you think about it. (same as "finished" - which I learned the hard way) Technically, "done" means it is already pushed to the gold silos ("silo" is something I'll get into in a second), and the client can confirm, rest assured, that everything is good from there - a "lgtm" response should do the trick.

Now, onto silos - which I really did not know at the very beginning. Don't try to make things into things they aren't - listen to what the person is describing to you, and as time passes, and as you work on tickets, you'll get to know what each component of a description is, and what the big picture is in and of itself. Now, a long time ago, all services were deployed on Metal; meaning that they exist in a real, physical database in Gameloft. Now, we're trying to push everything to the cloud, and as Newman said, it's rough - APACloud was one of the first to be pushed, and it cost a year of work and many sleepless nights. So not great. As Gameloft moves to more online platforms, we'll hopefully remove these metal silos completely - but since they are partially online, AND several services in cloud silos depend on Metal silos, it wouldn't work out if we got rid of them right now. On the new silos, built with AWS, services become more independent from one another.

Gist: Silos have services running on them. A silo has many services, each silo has a "pandora" service which is, rather "meta" as Ali put it - a service discovery service. It tells you what service - Janus, Anubis, Osiris, etc, - to go to. From there, if you're on Metal, you go to a new URL. Otherwise, if you're on the cloud, you follow what's called "path-based routing" which just runs you further down the tree of an HTTP(S?) URL. Maybe not that much of a gist I guess. Oh well. Here: Silos are an environment or datacenter where all of our services run for a particular game - some are for testing, some are for games - production is called Gold, when it’s actually live. (More specifically - Alpha is for testing, Beta is for more thorough testing after the groundwork and specifications are laid out. We can't deploy anything to Beta on Fridays. Gold is production - we are actually having clients use these services)

Problem is, our services are not built for the cloud. We have a heavy dependence on our services at Gameloft, which require crucial elements like authentication (Janus service), etc. As stated, we're adapting to the cloud. It's where everyone else is moving. "Spot instances" are a convenient element in the cloud - there's no guarantee they're great but they are **available** 24/7.

Something interested Anna mentioned was that each person has 3 hours on Thursdays and Fridays to learn some technology and get legitimate certification for it - like AWS, or the new hip Kubernetes software. K8s are huge in the industry now. It's all through Linux's learning system, but there's also PluralSite, where you can learn things like management, or languages.

Now, down to tasks. I attended a sprint planning session this week too, everyone dreads it, but it's kind of the thing that must be done. It takes half an hour, this time it took an hour at least, and they went over what needed to be implemented on a realistic time frame. I also got nicknamed "J", which I don't really like. But whatever, lol..

We have daily standups at 1:30. They last max half an hour, unless sprint planning is right after. We also call it SCRUM. You can call people out on things that you could work on, and also call them out in general, which can be funny - and rough.

### Tech Stack

Anubis deplots servers for games, and keeps track of waht player is joining which room, etc. We have a Controller that keeps track of processes for our game services, and a Lobby services that communicates with the controller and finder, keeping track of people in the room. I remember these were in their own separate files in Gurprit's introductory presentation of the Federation. Anubis was Gameloft's first online service.

### SSO

Ali told me that a generated SSO key ties your computer to Gitlab or Github. If the key matches, every time you do something "big"-ish, like push to the origin, you don't have to enter your username and password. You generate a key from your local, and paste it into the remote website. Simple liek that. Patrick taught me a cool command, push origin +HEAD which pushes everything on my current branch to the remote repo's version of that branch.

### SQL, Services and Database Services

I learned that SQL is a table-row-column database; essentially, it requires a lot from you to store data inside of it. In a noSQL database, this is not the case. You can send in a document, a link, and whatever format it'll be in, it'll accept. I believe he said that MongoDB and Couchbase are of these types. They just accept JSON entries - which are way less rigid, I mean, you can put whatever you want in it, while SQL will complain that you're missing a certain parameter or whatever.

Turns out you can SCALE your capacity to to deliver requests. Once you set up a "micro-service", that micro-service can run into the hundreds and thousands of requests. Millions, whatever. This next part is cut and pasted:

Scaling capacity - Let's take facebook for example. There are so many services Facebook has! All these services are deployed separately, the reason for which being, if say the authentication service goes down, then everything else will be okay. This'll minimize the impact of something being down. Each of these services will have different needs in terms of what they request from their hardware; they will serve a different number of requests. (e.g. one doesn't have to deploy multiple nodes of a service because the demand is low) Smart databases replicate a service to exist many times. However, they don’t store data inside a service, they store it inside a database. These 10, say, services are reaching out to the same database service, which will now be overwhelmed. This is not ideal. What we do is replicate the database services, so 1 or 2 instances of a service has a 1:1 ratio or two services are sharing one database service. Now that you have 10 photo services and a 1:1 ratio (10:10), these 10 databases need to share and replicate data amongst them.

What load-balancers will see, is that this instance of the photo service is not overwhelmed. Thus, it'll re-think it's replications, and not have to store so many. What NoSQL databases do is be redundant, so information is always highly available if something goes wrong.

### Kubernetes

Difference between a docker machine and virtual machine is subtle. The idea is the same - you can have multiple virtual machines on the same computer, each with the same deployment settings (how much CPU you can use, disk space, etc.)

Say you spin up two Docker containers which have two different servers, that have conflicting dependencies; i.e. this service in container 1 and this service in container 2 can't work under the same environment, so they don’t and fundamentally can't exist on the same machine.

Docker image - is a snapshot of an operating system - an environment (inclusive of everything, literally **everything** in an environment) which has the exact things you need to run a service. Because I know what services I need to run on this container - I'll isolate the requirements of a service, telling the container - and give instructions on exactly how I'm gonna make you work in this environment.

We can thus send services in Docker containers.

### Python virtual environments

Multiple apps can have different dependencies so you want to isolate them completely so they won’t mess with each other. They can communicate in the meantime, via a portal.
Python virtual environment is kind of the same thing, installing our dependencies in isolated places. This is not in a set environment - rather, things will go into a very generic place to install those dependencies. If you have two projects that have different dependencies, you use a virtual environment (our virtual environment called fed). We can run our services in (fed) by typing: source fed bin/activate, and (fed) will be activated. We have many dependencies inside fed/lib that we write out, and Python will look for dependencies under the fed workspace.

If you’re not in the fed environment, the services will not run because all the dependencies are in the fed folder under /workspace (the storage space of the fed virtual environment) This has a python link (a soft link) that links to a version of Python (I think?)

### Jidoka

Jidoka is the name that Gameloft gave to their cloud silos - silos that are running ENTIRELY on the cloud. They use path-based routing to eliminate calls to Pandora - meaning that whenever everything is moved to the cloud, Pandora will be obsolete. Their Metal silos include BOB, CAD, EUR, ASA, APA, CHIN, ANA, MDA, and MDB.

They also have Staging and Production silos, which are kubernetes silos that run on Metal. They are used for testing.

Then there are the Jidoka or cloud silos - Lego, Gangstar, Apacloud, and Common Beta. All of these silos run on AWS. There was then something about a jump host - tls-dev that allowed us access. (?) On this jump host, supposedly, we then hain access to all of our silos.

Kubernetes allows you to see all these pods, pods each of which correspond to one of the pods here (on fed-int-istio.common-beta)

### Kubernetes and the Release Process (?)

First of all, packages. Packages are made when our code gets pushed. Basically, when it gets pushed, it gets packaged. This package is a version of our code that is running. We create a Docker image out of the code by running it through a pipeline. This image is what we will launch. The first question is, can we build a Docker container - which are the first two tests. Second, can we create the Docker image? Third, can we put it into Harbor? Now, on Harbor - this is Gameloft's equivalent of Docker Hub. The convention is: make an image, give the name of the image and "tag" of the image. Push that image to Harbor, where we save our images. When you build a Docker image, you need to keep it somewhere. So build the image, push it to the repository, and then, you can run the image locally by doing "docker pull harbor.gameloft ..." (The reason we run it locally is to debug; get the image, run it locally, and see if the bug happens locally as well - then we can start debugging. This applies to production-level stuff as well) This produces a stretch "code" (a sequence of numbers). ANNND now, our goal is to link this Docker image to Kubernetes. Somehow. But first, what is Kubernetes?

### Kubernetes

Kubernetes is an orchestrator for Docker. It uses the architecture of a Jidoka silo to maintain it. When we deploy services, we have two different ways to deploy them - using Debian or Docker for our packages (?). When we release them, we use Docker and Helm - a Docker file is used to run the program in a container, while helm manages this and installs it. Kubernetes uses the architecture of a Jidoka silo; we make our services into Docker images, and use Kubernetes to orchestrate/aintain it. All of our cloud silos run with Kubernetes, and they in turn run Docker images.

Gist: Kubernetes maintains Docker images, or "runs" them. We have two different ways to deploy - either by Debian or Docker for our packages. When we release these packages (?) (what does release mean?), we use Docker and Helm. A Docker file is used to run the program (what is the program we are running - what is RUNNING in those Docker images?) while helm manages this program and installs it.

How do we link our Docker images to Kubernetes?

We use something called Helm. Helm is very similar to pip (in Python), where we search for charts. There are public charts and private charts. We link this image to a "helm chart version". By pinning a number to a Docker image, this tells Kubernetes what to run. (? is this the version number?) - by taking this number as a chart number, and knowing that chart numbers link to Docker images, using this number (the new version number), you run Kubernetes. Kubernetes will now go and find that image.

When the number changes, the pods change. It restarts. But more importantly, the Docker image changes.

Gist: Docker runs images in containers. Kubernetes runs containers in pods.

We say, "This pod (? what is a pod?) is running this image that was built in the pipeline." (We then did a brief overview of Ingres, which are a set of rules that thells Kubernetes what to do with all the incoming traffic)

-- end of first week
