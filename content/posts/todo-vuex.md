---
title: "The making of Todo App using Vuex"
date: 2018-10-15T21:05:00+09:00
draft: false
---
# Its has been a while since my first post
I've to commit that Im kinda lazy lately

Okay..Enough trash talk
So I've bee working with VueJs for a while which is very cool.
But the more I work with VueJs, the more I realize that I need a "state management system" cause everytime I break down the components and add actions into them...It become really messy

So I decided to learn [VueX](https://vuex.vuejs.org/)

And for me, the best way of learning something is to build something else using things that you want to learn.
So, I build a simple todo-app with VueJs and Vuex.Hooray...

I've put all the source code [todo-vuex](https://github.com/bachdx2812/todo-vuex)

## Init (2018-10-15)
So I built a very simple app with VueJs DONE

Here the screenshot of source code
![](https://imgur.com/ipdQafg.png)

#### What I've learned:
- Vuex seems nice, it makes the workflow looks better and the whole app's data more consistency.
- It makes source codes WAY more complex and harder to understand for sure. But still I have to commit that it will reduces the whole `this.$parent.$emit` things which I did a lot in the past (which I hate so much)
- ...(to be continued)

#### What I've realized:
- The source code is okay, I think. But it only for tiny apps which has only 1-2 sorts of data (items in todo for example)
![](https://i.imgur.com/GmrL0py.png)
As you can see above image, imagine we have 10 kinds of `state`. Each kind has 2-3 methods... Okay im quit..
So what im gonna do next is to make sure the `doom day` is not gonna happen.. by splitting the current `store/index.js` out.

Ref: https://markus.oberlehner.net/blog/how-to-structure-a-complex-vuex-store/
- ...(to be continued)


