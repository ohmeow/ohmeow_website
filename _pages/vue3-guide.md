---
layout: page
title: Vue 3 Guide
permalink: /guides/vue3
exclude_from_header: true
---

## Core
- - -
### Watchers / WatchEffect
#### **> How to I define an asynchronous watcher or watchEffect?**
```javascript
import { ref, watch, watchEffect } from 'vue'
import { useRoute } from 'vue-router'

export default {
  setup() {
    const route = useRoute()
    ...
    // watch
    watch(route, async (nv, ov) => {
      const { data } = await api.get(`get-something/blah`)
      console.log(data)
    })
    
    // watchEffect
    const stateChanged = watchEffect(async () => {
      const { data } = await api.get(`get-something/blah`)
      console.log(data)
     })
     ...
```
#### **> When should I use `watch` or `watchEffect`?**

Use `watch` when ...
1. You want to do something with one or more specific reactive objects changes
2. You need both the old value and the new value
3. You need it to be called lazily

Use `watchEffect` when ...
1. You want to do something whenever the state changes for any of your reactive objects
2. You don't care about the old value(s)
3. You need it to run immediately when reactive dependencies change

See: \
[Vue 3 Composition API - watch and watchEffect](https://www.thisdot.co/blog/vue-3-composition-api-watch-and-watcheffect) \
[How to use Vue Watch and Vue watchEffect](https://learnvue.co/2019/12/a-simple-vue-watcher-tutorial-for-beginners/)

- - -

### Routes

#### **> How can I pass data between routes using `params`?**

Simply add the data to your `params` attribute:
```javascript
<router-link :to="{ name: 'my-named-route', params: { id: 1, another_param: 'something else' } }">
Go to my page
</router-link>
```
See: \
[Vue, is there a way to pass data between routes without URL params?](https://stackoverflow.com/questions/50998305/vue-is-there-a-way-to-pass-data-between-routes-without-url-params)
