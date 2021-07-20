<template>
  <div class="
  bg-light-400 rounded p-1 px-5 text-[#7776] my-2 
  before:(content absolute block w-1 h-6 rounded-full bg-yellow-200 ml-[-16px])
  dark:(bg-dark-700)
  before:(dark:bg-dark-300)
  question-list transition-color
  hover:(text-current) cursor-help
  "
  tabindex="1"
  v-motion :initial="{ x: 980 }" :enter="{ x: 0, transition: { delay: seq * 800 + 500, duration: 1600}}">
    <slot>Question</slot>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  props: ['seq']
});
</script>

<style>
.question-list{
  @apply focus:(ring ring-yellow-300 text-current outline-none);
};
</style>
