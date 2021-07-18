---
title: Composition API - Vue
theme: default
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
monaco: false
fonts:
  # basically the text
  sans: "teko"
---

<div class="
  flex items-end justify-center gap-5 px-10 py-6 
  rounded-xl backdrop-filter backdrop-blur backdrop-brightness-60
  border-t border-t-gray-600
  border-l-[1px] border-l-dark-100
  shadow-xl
"
>
  <h1 class="!mb-0 font-teko">Composable Vue</h1>
  <div class="mb-4">Brand new method to work with vue</div>
</div>

<div class="pt-12">
  <button @click="$slidev.nav.next" class="border inline-flex justify-center items-center px-4 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Start <carbon:arrow-right class="inline ml-2 text-sm"/>
  </button>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

# Composition API?

Vue2 composition api plugin / Vue3, Vue2.7 native

> Composition is a new concept addressing the following problems with Vue2 Optional API and Mixin.

<div class="grid grid-cols-3 gap-3 my-2">
<Card title="This reference" v-click>
  Option api dynamically bind <code>this</code> to instance, TypeScript and IDE hate it.
</Card>
<Card title="Spaghetti Code" v-click>
  When component get large, same logic code will scatter around your options
</Card>
<Card title="Unknown Mixin" v-click>
  Code reusing is difficult through mixin since it's auto merge, you need to know exactly mixin provided options.
</Card>
<Card title="Mixin Name" v-click>
  Mixin name is conflict prone due to option merge.
</Card>
<Card title="Mixin Trace code" v-click>
  Mixin properties seem to came from nowhere
</Card>
<div class="flex flex-col justify-end" v-after>
<div class="inline-block text-gray-400">Extra reading:</div>

- [Why composition API | Vue3.js](https://v3.vuejs.org/guide/composition-api-introduction.html#why-composition-api)
- [VueUse - Composition Library<br>(Vue2 support!)](https://vueuse.org/)
</div>
</div>


---
layout: image-right
image: /src/compare.png
---

# Options API

A <span class="font-black">counter</span> and a <span class="font-black">books list</span> fetch logic snippet

```js {all|1-5|6-9|10-13|14-19|2,7,11,12|3,4,8,15-17}
data(){
  count: 0,
  books: [],
  loading: true,
},
computed: {
  canResetCount(){ return this.count === 0;},
  sortedData(){ return [...this.books].sort();},
},
method: {
  addCount(){ this.count += 1;},
  resetCount(){this.count = 0;}
},
async mount(){
  this.loading = true;
  this.book = await api.getBooks();
  this.loading = false;
}
```


---

# Composition API

A <span class="font-black">counter</span> and a <span class="font-black">books list</span> fetch logic snippet

```ts
import { ref, computed, unref, defineComponent } from 'vue';

/** Sound's like you need documentation? */
const useCounter = () => {
  const count = ref(0)
  const addCount = () => {count.value += 1}
  const resetCount = () => {count.value = 0}
  const canResetCount = computed(() => unref(count) === 0)
  return {count, addCount, resetCount, canResetCount}
}

export default defineComponent({
  setup(){
    const {count, addCount} = useCounter();
    return {
      count, addCount
    }
  }
})
```


---


# Reuse Code

<div grid="~ cols-2 gap-4">
<div>

```ts
import { defineComponent } from "vue";
import { useMouse } from "@vueuse/core";

export default defineComponent({
  setup() {
    const { x, y, sourceType } = useMouse();
    return { x, y, sourceType };
  },
  template: `
  <div>
    <h3> Tracking your {{ sourceType }} </h3>
    <div>x: {{ x }} </div>
    <div>y: {{ y }} </div>
  </div>
  `
});


// padding
```

</div>
<div>

<MouseTrack />

</div>
</div>

---

# Behind the scene
The brand new reactive system

