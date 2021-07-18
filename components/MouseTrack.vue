<template>
  <div class="h-full w-full bg-light-400 p-6 flex flex-col gap-3">
    <h3>
      Tracking your <b class="!text-light-blue-700">{{ sourceType }}</b>
    </h3>
    <div class="inline-flex p-2 border rounded font-mono">x: {{ x }}</div>
    <div class="inline-flex p-2 border rounded font-mono">y: {{ y }}</div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import { useMouse } from "@vueuse/core";

export default defineComponent({
  setup() {
    const { x, y, sourceType } = useMouse();
    return { x, y, sourceType };
  },
});
</script>
