---
layout: page
title: Vue 3 Guide
permalink: /guides/vue3
exclude_from_header: true
---

## Core
- - -
### Computed properties
#### **> How to I define a computed property using the Composition API?**
```javascript
// just a getter
const userEmail = computed(() => {
  return $store.getters.userEmail
})

...

// a getter and setter
const selectedUserClientId = computed({
  get: () => {
    return $store.getters.selectedUserClientId
  },
  set: (newVal) => {
    $store.dispatch('setSelectedUserClientId', { client_id: newVal })
  }
})
```
See: \
[How to type a computed property in the new composition API?](https://stackoverflow.com/a/64281689) \
[How to call setter for object in computed properties](https://forum.vuejs.org/t/how-to-call-setter-for-object-in-computed-properties/29177) 

---

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

- - -

### Vuex

#### **> How can I watch for changes in the store's values?**

Simply add the data to your `params` attribute:
```javascript
setup(props) {
   const store = useStore();

   watch(()=>store.getters.myvalue, function() {
      console.log('value changes detected');
   });

   return {
      myvalue: computed(() => store.getters.myvalue)
   }
},
```
See: \
[Vue3 composition api watch store value](https://stackoverflow.com/a/67776890) 

#### **> How can I watch for changes in the store's values *across browser tabs and windows*?**
```javascript
const app = new Vue({
  el: '#app',
  data: {
    name: ''
  },
  methods: {
    onStorageUpdate(event) {
      if (event.key === "name") {
        this.name = event.newValue;
      }
    }
  },
  mounted() {
    if (localStorage.name) {
      this.name = localStorage.name;
    }
    window.addEventListener("storage", this.onStorageUpdate);
  },
  beforeDestroy() {
    window.removeEventListener("storage", this.onStorageUpdate);
  },
  watch: {
    name(newName) {
      localStorage.name = newName;
    }
  }
});
```
See: \
[Reactive localStorage object across browser tabs using Vue.js](https://stackoverflow.com/a/52782774) 

#### **> How can I store complex objects like arrays and dictionaries in localStorage?**
By using `JSON.stringfy(X)` when storing the data and `JSON.parse(X)` when you fetch the data
```javascript
var names = [];
names[0] = prompt("New member name?");
localStorage.setItem("names", JSON.stringify(names));
var storedNames = JSON.parse(localStorage.getItem("names"));

// ... or ...
localstorage.names = JSON.stringify(names);
var storedNames = JSON.parse(localStorage.names);
```
See: \
[How do I store an array in localStorage? ](https://stackoverflow.com/questions/3357553/how-do-i-store-an-array-in-localstorage) 

- - -

## Quasar
- - -
### Working with `q-table`
#### **> How can I create grid for CRUD operations using a modal form for inserts/upserts with filtering, sorting, etc...?**

See: \
[QTable with Action Buttons](https://codepen.io/metalsadman/pen/ZgKexK?editors=1010) \
[Quasar QTable: Editing with QPopupEdits and QButtons to add/delete/update rows](https://codepen.io/mickey58/pen/eYYVqWv?editors=1010) \
[Quasar - q-table with toggle filters and text search](https://codepen.io/b0otable/pen/PozWLYR) 

