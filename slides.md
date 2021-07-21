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
fonts:
  # basically the text
  sans: "teko"
---

<div class="
  flex items-end justify-center gap-5 px-10 py-16 
  rounded backdrop-filter backdrop-blur backdrop-brightness-60
  border-t border-t-gray-600
  border-l-[1px] border-l-dark-100
  shadow-xl
"
>
  <h1 class="!mb-0 !text-4xl tracking-[6px] uppercase font-thin">Composition API</h1>
  <div class="mb-1 tracking-[1px] text-gray-200">Brand new method to work with vue</div>
</div>

<div class="pt-12">
  <button @click="$slidev.nav.next" class="border inline-flex justify-center items-center px-4 py-1 rounded cursor-pointer tracking-[4px] uppercase text-xs" hover="bg-white bg-opacity-10">
    Start <carbon:arrow-right class="inline ml-2 text-sm"/>
  </button>
</div>

<div class="abs-br m-6 flex gap-2 items-center">
  <span text="xs gray-400">Full experience of type support by monaco-editor in dev mode</span>
  <a href="https://github.com/hikariNTU/composition-api-slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white"
    title="Slidev Slide - Composition API intro - Github">
    <carbon-logo-github />
  </a>
</div>



---
layout: image-right
image: /compare.png
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


# What can Composition API help?

Vue2 composition api plugin / Vue3, Vue2.7 native

<!-- > Composition is a new concept addressing the following problems with Vue2 Optional API and Mixin. -->

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
<Card title="Life Cycle" v-click>
  Life cycle from vue is directly bind in option.
</Card>
<div class="flex text-right justify-end items-center text-gray-600 pr-3 border-r" v-after>
Extra Reading
</div>
<div class="flex flex-col justify-end col-span-2" v-after>

- [Why composition API | Vue3.js](https://v3.vuejs.org/guide/composition-api-introduction.html#why-composition-api)
- [VueUse - Composition Library (Vue2 support!)](https://vueuse.org/)

</div>
</div>


---

# Composition API (counter)

A <span class="font-black">counter</span> and a <span class="font-black">books list</span> fetch logic snippet

```ts {monaco}
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

# Composition API (book list)

A <span class="font-black">counter</span> and a <span class="font-black">books list</span> fetch logic snippet

```ts {monaco}
import { ref, computed, onMounted, defineComponent } from 'vue';
const api = {async getBook(){return ['hello', 'world']}}
const useBookList = () => {
  const loading = ref(true)
  const book = ref([''])
  const sortedBook = computed(() => [...book.value].sort())
  onMounted(async() => {
    loading.value = true
    book.value = await api.getBook()
    loading.value = false
  })
  return {loading, book, sortedBook}
}
export default defineComponent({
  setup(){
    const { loading, book } = useBookList();
    return { loading, book }
  }
})
```

---

# Composition API - props and context

Since `setup()` is actually `created()` hook, component instance won't be ready for use

<div grid="~ cols-2 flow-col" class="gap-4 grid-rows-[auto,1fr]">

### Props

```ts {monaco}
import { computed, defineComponent } from 'vue';
export default defineComponent({
  props: ['title', 'count'],
  setup(props){
    // First arg is props, which is "reactive"
    // You should not destruct it directly
    const displayName = computed(
      () => `${props.title} ${props.count}`,
    )
    return { displayName }
  }
})



// padding
```

### Context { emit }

```ts {monaco}
import { defineComponent } from 'vue';
export default defineComponent({
  // You can define your emit in Vue3 just like props
  emit: ['clicked'],
  // The second is context, a plain js object
  setup(_, { emit, slots, attrs }){
    const onBtnClick = () => {
      emit('clicked', 'Hello click!!')
    }
    return { onBtnClick }
  }
})



// padding
```


</div>


---

# Reuse Code

<div grid="~ cols-2 gap-4">
<div>

### Confidence on useComposable

```ts {monaco}
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

### Result

<MouseTrack />

</div>
</div>

---

<div class="h-full grid grid-cols-[2fr,1fr] grid-rows-[1fr,auto]" >

```ts {monaco}
import { 
  computed, defineComponent, onMounted, ref, unref, watch
} from "vue";

// This thing is share as module level.
const count = ref(0);

export default defineComponent({
  setup(){
    const addCount = () => { count.value = unref(count) + 1 };
    const reset = () => { count.value = 0 };
    const noReset = computed(() => unref(count) === 0);

    // assign the count to global js
    onMounted(() => {
      globalThis.myCounter = count;
      globalThis.watch = watch;
      globalThis.computed = computed;
    });

    return { count, addCount, reset, noReset }
  }
});
```

<Counter />
<div class="mt-4 text-center !text-dark-100 col-span-full animate-pulse">
<code>myCounter</code> is exported to global !!
Open your browser console to find it
</div>
</div>


---

# Composition Pros & Cons

| **Pros**                                  | **Options API**                                    |
| ----------------------------------------- | -------------------------------------------------- |
| Clear Code Logic                          | Bind to options scattering around your component   |
| Strong type support by natual             | Need extra decorator or type indicator             |
| Easy to reuse/test since it's function    | Reuse need extra careful and fully document        |
| Ability to control Lifecycle hook         | What you see in lifecyle is what you get           |
| Almost no constrain on how you write code | options need to follow some js specified this rule |

---

# Composition Pros & Cons

| **Cons**                                                    | **Options API**                                      |
| ----------------------------------------------------------- | ---------------------------------------------------- |
| obj.value is not standard js                                | this.obj is standard js                              |
| Extra careful about it's reactive                           | Extra careful about it's setter/getter               |
| Cannot stub data in Vue test utils                          | Stubbing whatever you want in VTU (Bad practice BTW) |
| No clear life cycle go through                              | Template follow these options                        |
| Can potentially write code that's more terrible than option | Can't get wrong since it just don't work             |

---
layout: center
preload: false
---

# QA?

<span v-motion-fade>In case you don't know what to ask:</span>

<Question :seq="1">Is the idea of composition API come from vue3?</Question>
<Question :seq="2">Only Vue3 can use composition API?</Question>
<Question :seq="3">Is Composition API or Hook API the same thing so-called Functional Programming？</Question>
<Question :seq="4">How does Composition API work?</Question>
<Question :seq="5">Can I keep optional API style?</Question>
<Question :seq="6">Composable Best Practice?</Question>

---

# Appendix

<div grid="~ cols-2">
<div>

- [Reactivity in Depth | Vue.js](https://v3.vuejs.org/guide/reactivity.html)
- [Vue 3 Reactivity | Vue Mastery](https://www.vuemastery.com/courses/vue-3-reactivity/vue3-reactivity/)
- [Composable Vue | Anthony Fu](https://talks.antfu.me/2021/composable-vue/)
- [可組合式 Vue | Anthony Fu (上面的中文版，比較詳細 ^ ^)](https://talks.antfu.me/2021/vueconf-china)
- [Mixin problem (中文) | Dennis Chung](https://hackmd.io/@hikari1286tw/Hyqwf40pd)

This guy is god:

<div class="inline-flex items-center gap-2 border px-6 py-4 rounded">
<img 
  class="w-16 h-16 rounded-full flex-shrink-0"
  src="https://avatars.githubusercontent.com/u/11247099?v=4"
/>
<div>
<h3 class="!pt-0"> Anthony Fu </h3>
<span class="text-sm"> Vue3, Vite, VueUse and SliDev</span>
</div>
<div>
<a href="https://github.com/antfu" target="_blank" alt="GitHub"
  class="text-xl icon-btn opacity-50 !border-none">
  <carbon-logo-github />
</a>
</div>
</div>
</div>

<div class="flex gap-4">
<Card title="vite + vue3 + windicss startup">
<div class="flex justify-center">
<a href="https://github.com/hikariNTU/vue-new-feature" target="_blank" alt="GitHub"
  class="text-xl icon-btn opacity-50 !border-none">
  <carbon-logo-github />
</a>
</div>
</Card>

<Card title="Vue2 plugin for composition api">
<div>
Official: <a href="https://github.com/vuejs/composition-api" target="_blank" alt="GitHub"
  class="text-xl icon-btn opacity-50 !border-none">
  <carbon-logo-github />
</a>
</div><div>
Vue demi: <a href="https://github.com/vueuse/vue-demi" target="_blank" alt="GitHub"
  class="text-xl icon-btn opacity-50 !border-none">
  <carbon-logo-github />
</a>
</div>
</Card>
</div>
</div>