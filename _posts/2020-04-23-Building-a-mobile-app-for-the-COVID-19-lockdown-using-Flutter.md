---
layout: post
title: Building a mobile app for the COVID-19 lockdown using Flutter  
tags: mobile app flutter coronovirus 
---

###  TL;DR
This post is about a mobile app I developed called 13033 using Google's Flutter for simplyfying the process of registering your movement (by sending the required SMS to 13033) when leaving your house during the COVID-19 lockdown in Greece. The app has already **more than 6.5K downloads** (as of April 23) and can be found on [**Play Store**]([https://play.google.com/store/apps/details?id=metakinisi.app](https://play.google.com/store/apps/details?id=metakinisi.app)).
  

###  Leaving home during the Covid-19 Lockdown

The world is going through really difficult times because of the COVID-19 pandemic. We are daily facing a new reality with big changes in the way we live, work and interact. And it seems that these changes will not be that temporary after all and probably be part of the new 'normal'.

Greece imposed a nationwide lockdown on March 23. People were only allowed to leave their house for specific reasons and only after registering their movement in advance either by filling out a form or by sending an SMS with a predifined structure to 13033.

There are six available/allowed reasons: 
 1. Visiting a pharmacy or a doctor
 2. Trips to supermarkets, bakeries or kiosks 
 3.  Visiting a bank, if electronic transactions can't be made
 4. Visiting relatives in need
 5. Attending weddings, baptisms or funerals
 6. Exercising outdoors or walking a pet

and the SMS structure should be like this: 

						_X [space] Name [space] Surname [space] Address_
where X represents the number that corresponds to one of the above options.

Easy right? Sure... if you are [millennial]([https://en.wikipedia.org/wiki/Millennials](https://en.wikipedia.org/wiki/Millennials)) or even younger. It turns out that what is easy for you could be really hard for others, especially older ones like your mother or grandparents. 

Therefore, I thought of creating a simple app for simplyfying the process. It was not something hard to build since I had built a [mobile app]([https://play.google.com/store/apps/details?id=com.dpaxinos.adalert_mobile&hl=en](https://play.google.com/store/apps/details?id=com.dpaxinos.adalert_mobile&hl=en)) before, but turned out to be really useful. 

I developed it using Google's [Flutter]([https://flutter.dev/](https://flutter.dev/)) framework which I highly recommend. It is easy to pick up and you can become quickly very productive. 

### How does it work?
 - The user first has to fill in her name and adress which is stored locally on the device. No personal data leaves the phone and the app is GDPR compliant. 
 - On the next screen, the user selects the option for your movement. Once the selection is made, the messaging application gets launced with prefilled the generated message. 
 - The design is simple on purpose; large buttons and clear layout to avoid any possible confusions or misinterpretations.
 - The option of automatically sending the SMS without entering the SMS app was rejected because of the additional permissions that the app would have needed and often scare people.
  

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/13033/13033_two_screens.jpg)

The app was also presented in an [article](https://www.thetoc.gr/koinwnia/article/koronoios-13033---i-dorean-efarmogi-pou-stelnei-ta-sms-metakinisis-me-3-klik/) on a greek news site and providing some publicity. Now, after less than a month, it has reached more than 6.5K downloads and has helped many people in their daily life. 

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/13033/13033_Stats.JPG)

### What I got out of it?
- Got the satisfaction of building something that helps and is being used by more than 6K people. 
- Discovered that even the simplest app can cause confusions since
- I had to do a lot of support to people contacting me with various questions about the app and its use.

I really hope that the lockdown comes to an end very soon, but until then, please feel free to [download]([https://play.google.com/store/apps/details?id=com.dpaxinos.adalert_mobile&hl=en) and use the 13033 app. 


