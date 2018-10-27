---
title: "The making of Todo App using Vuex"
date: 2018-10-15T21:05:00+09:00
showDate: true
tags: ["petproject", "programing", "js", "vuejs", "vuex"]
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

Ref: http://chibinowa.net/note/vuejs/vue-14.html

## Vuex Modules (2018-10-27)
Luckily for me, Vuex actually has a nicely way to deal with my problem
[Vuex Modules](https://vuex.vuejs.org/guide/modules.html)
So as the document said
```
To help with that, Vuex allows us to divide our store into modules. Each module can contain its own state, mutations, actions, getters, and even nested modules
```

So first thing I need to do is just split `todo-item` into `store/modules/todoItem.js`
and then move all the code inside store inside it.

Which looks like this:
![](https://i.imgur.com/CixVely.png)
And the main component with `items` will looked like this
```javascript
computed: {
  items: function() {
    return this.$store.state.todoItem.items;
  }
}
```

Let's check again to see if it still work!
...
It's work perfectly the same way.OK for now.

But the code is...smell.Why ? Because let think about when we need to deals with the `filter` datas, you have to deal with it like this all the time? I think I need to figure out the better way to do it.

I'll comeback soon to deal with this.

### Vuex Getters
[Vuex Getters](https://vuex.vuejs.org/guide/getters.html)

Imagine when you have lots of components, and each one of them would use the filtered list of items.
With the style I've done, I have to repeat in every single components, which I dont really want to.
So, How would I avoid this.

The concept of `vuex getters` is created for exact same purpose
```
Vuex allows us to define "getters" in the store. You can think of them as computed properties for stores. Like computed properties, a getter's result is cached based on its dependencies, and will only re-evaluate when some of its dependencies have changed.
```

So I re-write my code base on this. How would it be?

First, the todoItem.js. Add this getters block
```javascript
getters: {
  itemList: state => {
    return state.items;
  }
},
```
And then the usage
```javascript
computed: {
  ...mapGetters({
    // map `this.items` with `this.$store.state.getter.itemList`
    items: 'itemList'
  })
}
```

Damn, this looks so much better, right?
