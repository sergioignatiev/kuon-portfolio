<template>
  <div class="mt-5">
    <ul class="flex flex-row gap-5 flex-wrap">
      <li
        v-for="(value, index) in tagSettings"
        :key="index"
        class="tags lg:text-md text-sm text-center selector rounded-md xl:p-3 xl:px-4 p-2 px-3 cursor-default transition ease-in-out hover:rotate-6"
      >
        {{ value }}
      </li>
    </ul>
  </div>
</template>

<script setup>
const props = defineProps({
	tagSettings: {
		type: Array,
		default: () => []
	}
});
</script>

<style scoped>
  .tags:hover {
    color: var(--text-highlight-2);
  }
</style>
