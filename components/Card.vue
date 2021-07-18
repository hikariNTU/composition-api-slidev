<template>
  <article
    class="
      flex flex-col
      bg-white
      rounded-xl
      shadow-md
      border border-true-gray-200
      hover:shadow-xl
      transform
      hover:translate-y-[-0.2rem]
      transition
      dark:(bg-dark-400
      border-dark-100)
      dark:hover:(shadow-md
      shadow-light-800)
    "
  >
    <h2
      class="
        font-family-handwriting
        text-center
        mx-2
        mt-4
        mb-2
        !text-[1rem]
        text-cool-gray-600
        font-black
        dark:(text-cool-gray-400)
      "
    >
      {{ title }}
    </h2>
    <hr
      class="border-none bg-blue-gray-200 h-1 mx-4 rounded-full dark:bg-dark-50"
    />
    <div class="p-4 leading-6"><slot></slot></div>
  </article>
</template>

<script>
export default {
  name: "FieldCard",
  props: {
    title: {
      default: "Play Ground",
      type: String,
    },
  },
};
</script>
