---
title: "Chatbot development log"
date: 2018-11-05
showDate: true
tags: ["petproject", "programing", "js", "vuejs", "vuex", "nodejs"]
draft: false
---
This is actually gonna be the presentation of my 勉強会 for my colleagues
Source code: https://github.com/bachdx2812/support-bot

# The Goal:
For very long time (still happen today), the `user` while surfing the internet sometime has to fill a lot of `form` with tons of information
which kind of boring.
For example: Name, address, birthday, gender, ..blah blah blah
Which sucks

So actually this bot wasnt my idea, you can see a lot of similar chatbot on the internet nowaday. I myself has an freelance job offer for doing this, so I did try to make it. Not really perfect but I think it can be used and can be able to create much more bigger things like just fill a form.

But, lets just do it the simple way first.

So, the goal is to make a bot, which act like human being to perform tasks like this:

1. Say hello when user click on the `button` or `chat icon` or sth like that.
2. Ask for name
3. Ask for address ( Japan's address this time. )
  ##### TODO: making address to be configurable for other countries
4. Ask for gender
5. Ask for something user want from website (infos, documents, ..) which normal form would present in checkboxs
6. Ask for something user has to choose only 1 in multiple options which normal form would present in radio buttons
7. Ask for something user need to fill in which normal form would present in input
8. ...(to be updated)

# The technique:
1. Server side: NodeJs with expressJs (this time) or RoR (my freelance job) or whatever you want
2. Client side: VueJs (this time) or React or whatever you want

# Required:
1. Nodejs (Lastest. I always do lastest)
2. Yarn (I prefer yarn than npm)
3. [Vue Client](https://cli.vuejs.org/)
4. MacOS(mine) or Linux's would be recommended

# HandOn
After install vue-client, if there wasnt any problems then you should be able to do this in command line
```bash
vue create support-bot
```
And then
```bash
cd support-bot && yarn serve
```
Check in browser http://localhost:8080/

You would be able to see the default homepage like this:
![](https://i.imgur.com/NTVI8XZ.png)

Of course we will not use this template , so I will delete them all

The default template source code is in src/App.vue

First thing first, I will make a wrap component for the bot. Let's just call it `Bot.vue`
The Bot things would be in the bottom-right corner of the screen so let add some CSS

(...After few moments...)
After making up the css for a while. We will be able to see this simple chat like this:
![](https://i.imgur.com/xWz8D0U.png)
And the source code will look like this:
```js
<template>
  <div class="fabs">
    <div class="chat" :class="chatClass">
      <div class="chat_header">
        <div class="chat_option">
          <div class="header_img">
            <img src="https://res.cloudinary.com/dqvwa7vpe/image/upload/v1496415051/avatar_ma6vug.jpg">
          </div>
          <span id="chat_head">Jane Doe</span> <br> <span class="agent">Agent</span> <span class="online">(Online)</span>
        </div>
      </div>
      <div id="chat_converse" class="chat_conversion chat_converse" style="display: block;">
        <span class="chat_msg_item chat_msg_item_admin">
          <div class="chat_avatar">
            <img src="https://res.cloudinary.com/dqvwa7vpe/image/upload/v1496415051/avatar_ma6vug.jpg">
          </div>
          Hey there! Any question?
        </span>
        <span class="chat_msg_item chat_msg_item_user">Hello!</span>
        <span class="status">20m ago</span>
        <span class="chat_msg_item chat_msg_item_admin">
          <div class="chat_avatar">
            <img src="https://res.cloudinary.com/dqvwa7vpe/image/upload/v1496415051/avatar_ma6vug.jpg">
          </div>
          Hey! Would you like to talk sales, support, or anyone?
        </span>
        <span class="chat_msg_item chat_msg_item_user">
        Lorem Ipsum is simply dummy text of the printing and typesetting industry.</span>
        <span class="status2">Just now. Not seen yet</span>
      </div>
    </div>

    <a class="fab" @click="toggleState">
      <i class="prime zmdi" :class="fabClass"></i>
    </a>
  </div>
</template>

<script>
let STATE_INITIALIZE = 1;
let STATE_ACTIVE = 2;

export default {
  props: {
  },
  data: function() {
    return {
      state: STATE_INITIALIZE,
      fabClass: 'zmdi-comment-outline',
      chatClass: ''
    }
  },
  methods: {
    toggleState: function() {
      this.state = this.isInitializeState ? STATE_ACTIVE : STATE_INITIALIZE;
    }
  },
  computed: {
    isInitializeState: function(){
      return this.state == STATE_INITIALIZE;
    }
  },
  watch: {
    state: function() {
      this.fabClass = this.isInitializeState ? 'zmdi-comment-outline' : 'zmdi-close is-active';
      this.chatClass = this.isInitializeState ? '' : 'is-visible';
    }
  }
}

</script>

<style scoped>
@import '../assets/style/mainbot.css';
</style>
```

