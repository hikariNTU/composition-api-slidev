<template>
  <div class="m-8 flex flex-col flex-grow font-family-digit" role="application">
    <div class="text-sm text-warm-gray-600 text-center">
      <code
        class="
          bg-light-700
          pt-2
          pb-1
          px-4
          inline-flex
          mb-1
          font-family-digit
          animate-bounce
        "
      >
        Counter.vue
      </code>
      <p>Share state with reactive</p>
    </div>

    <div
      class="
        flex flex-grow
        justify-center
        items-center
        text-7xl
        font-black
        my-4
        mx-2
        text-gray-600
      "
    >
      {{ count }}
    </div>
    
    <div class="flex gap-4 mt-4">
      <button @click="addCount" class="btn-count">ADD</button>
      <button
        @click="reset"
        class="btn-count"
        :class="{
          'btn-count--reset': !noReset,
        }"
        :disabled="noReset"
      >
        RESET
      </button>
    </div>
  </div>
</template>

<script>
import { computed, defineComponent, onMounted, ref, unref, watch } from "vue";

const count = ref(0);
export default defineComponent({
  setup(){
    const addCount = () => {
      count.value = unref(count) + 1;
    };
    const reset = () => {
      count.value = 0;
    };
    const noReset = computed(() => unref(count) === 0);

    onMounted(() => {
      globalThis.myCounter = count;
      globalThis.watch = watch;
      globalThis.computed = computed;
    });

    return {
      count, addCount, reset, noReset
    }
  }
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap");
.font-family-digit {
  font-family: "Press Start 2P", cursive;
}

.btn-count {
  touch-action: manipulation;
  @apply border-[0.3rem] border-gray-300 h-[4rem] flex-grow text-xl font-bold;
  @apply transition tracking-wider;
  @apply select-none text-gray-500;
  @apply focus-visible:ring ring-gray-700 focus:outline-none;
  @apply not-disabled:(hover:bg-light-400 shadow-md);
  @apply disabled:(cursor-default bg-light-900);
  @apply active:(bg-light-800 shadow-sm);
  
}
.btn-count.btn-count--reset {
  @apply border-yellow-300 text-yellow-600;
}
</style>
