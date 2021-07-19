<template>
  <article
    class="
      flex flex-col
      bg-white
      rounded
      shadow-md
      border border-true-gray-100
      border-l-4px border-l-yellow-300
      hover:shadow-xl
      transform
      hover:translate-y-[-0.2rem]
      transition
      dark:(bg-dark-400
      border-dark-300)
      dark:hover:(shadow-md
      shadow-light-800)
    "
  >
    <h2
      class="
        font-family-handwriting
        mx-4
        mt-4
        !text-[1rem]
        text-cool-gray-600
        font-bold
        dark:(text-yellow-400)
      "
    >
      {{ title }}
    </h2>
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
