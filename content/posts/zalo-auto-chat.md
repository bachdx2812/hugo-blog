---
title: "The making of My Personal Support Bot"
date: 2018-10-27
showDate: true
tags: ["petproject", "programing", "js", "vuejs", "vuex", "nodejs"]
draft: false
---
Its 3am and I really feel sleepy right now.

# Purpose
I've been always impressed by [J.A.R.V.I.S](http://ironman.wikia.com/wiki/J.A.R.V.I.S.) in Iron Man movies.
But please dont get me wrong. Currently Im not good enough to build such an intelligent bot like that.
I just want a simple bot which do some simple `daily tasks` for me.
Because its gonna be fun isnt it?

## The first function(2018-10-27)
### The purpose
Im currently working far from my family (Im in Japan and my family back in VietNam).

I have a carring mother who always care about me. And I love her so much that I dont want her to worry about me all day long.
The thing is my mum always care about the time I arrive home when I finish my job, that I have to text her around 10pm~ everyday just to
let her know that Im home (even when I still be in the train or still working at that moment)

Sometimes I forgot to text her, which make she really worry.
Okay. Let's build an automatic `sending message` bot to send my mum messages.

This gonna be nodejs server side application
By the way me and my mum using an application called `Zalo` to send message.
So first thing first. I gotta find the `Zalo API`

Bingo : https://developers.zalo.me/docs/api/social-api/tai-lieu/goi-tin-nhan-toi-ban-be-post-1183

Lets do this.

#### First Trouble: (5am in the morning)
Seem like I need to regist an application in zalo and then request my mum to use that app in order to send messages to her.
And that not really the things I want.
Now Im waiting my mum to accept my app's request in order to test sending message. Damn...
Maybe I should do something else meantime.

Updated: 4pm: My mum clicked on the app request link I sent here before but nothing happened. I tried again but still doesnt work.
Maybe zalo api is not really good..
I will skip this.
By the way I still keeping the source code here just in case: https://github.com/bachdx2812/zalo-api

## The second function (2018-10-28)
### The purpose
Im using Spotify to listen to music while im working. Im thinking about using Spotify API to make my own music player on the chatbot.
