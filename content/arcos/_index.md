---
title: "Australian Research Container Orchestration Services (ARCOS)"
date: 2021-11-03T11:16:00+08:00
draft: false
---

# Why at UWA?

[ARCOS](https://arcos.ardc.edu.au) have been working with the national community with the aim of establishing a national Kubernetes service.

So straight off the bat I have thrown a product in your face. I could spend the next several paragraphs going over what Kubernetes (k8s) is but a simple search on
the Internet would provide you with more material on this that you could or would want to handle. Let's just say that this product falls within the Cloud category, 
is IT candy and all so good you will come back for more.

The CeRDS team have been active members of the ARCOS working groups for some time and have acknowledged the benefits that participation within this community can bring.
It is no secret that the concepts of "Cloud Native" and "Hybrid Cloud" are permeating in to all areas of information technology including supporting services for research.
What is usually missing is a plain explanation as to why... So here is my attempt.

1. The most powerful advantage IMHO is that the "Cloud", while conjuring up images of white fluffy unicorns, can with some wizardry, not only
   incorporate large scale Corporate base infrastructure but also (and wait for it) incorporate an edge service like a data collector (think IoT), server
   (what we in the IT industry lovingly call bare metal) dedicated to things like data pre-processing as well as your very own laptop. This essentially means
   that complex services running at multiple locations can be managed with better security and less overheads paving the way for systems that run where it makes sense.
   Trust me, this is very powerful and cool. It provides an environment where many traditional as well as new services and processes can thrive.
2. I'm not going to hand you the cool aid. Cloud services do not make a complex workflow easy but it does help to make them manageable.
   I foresee your sceptical gaze and do not blame you. While this topic alone can run into many pages I provide you some highlights for your consideration.
   1. Modularity between component parts of the service. Cloud services (micro services) compartmentalise functionality and standardise how these are accessed 
      resulting in a number of benificial effects:
      a. Work on one component will rarely impact it's dependancies leaving development and support operations to be done unhindered.
      b. Subject mater experts can do what they do well with minimal requirement to engage with other experts. Work can progress safer and faster. This point
         is where most researchers come in as this concept also applies. With a small amount of process a researcher can deploy code, tools, whatever, in many cases without
         having to continuously worry about resources, what type of storage is required, have tedious IT meetings, you know the stuff that is not research.
      c. Large scale Infrastructure, code and process re-use. Stand on the sholders of those before you and move forward. This is the point of it all is it not.
      d. I feel like I've started waffling so let's move on.
   2. Infrastructure as a service (IaaS). Lets take Kubernetes, this humble Cloud based thing supported in-house, provided via HPC services and/or purchased, can provide:
      a. Clustering to ensure your service or application runs with maximum uptime
      b. Auto scalling making sure that load on provided service is automatically taken care of
      c. Monitoring, log management, auditing to ensure things are running as expected and providing warnings if issues are imminent
      d. Security at many levels including automatic certificate management, data and communications encryption, authentication and authorisation for required services.
         Mitigation of common attach fronts. Audits to highlight suspect interactions. All the goodness that a securiy team gets exited over.
      e. So many more...
      Many of these happen transparently just by launching your code, service, application. As the application is now not directly responsible for these functions, which was not traditionally
      the case, the application selection or development is simplified (reducing time and potentially cost) and security is much tighter.
3. Many practices come along with this type of change. I'm going to rattle of some terms you may have heard, so here goes, Continuous Integration and Continuous Deployment (CI/CD),
   DevSecOps (shortened from the words Development, Security, Operations), Infrastructure as Code (IoC). There are many more but you get the point. All of these terms mean
   pretty much the same thing, faster, safer, cheaper, more consistent outcomes starting from the formation of an idea all the way to the end product including support. Sound
   like something you would be interested in?
4. As stated already there is so much more but I'm hoping the point is made and you are on your way to becoming convinced.

This community has been investigating the benefits of Cloud Native and Hybrid Cloud service to better support research for some time 
and have come up with a number of services that the CeRDS team consider essential to the long term support of research activities.
