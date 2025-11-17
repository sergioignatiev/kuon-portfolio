<template>
  <section class="flex sm:flex-row flex-col lg:pt-10">
    <!-- Left side navigation-->
    <div class="flex flex-row sm:flex-col mt-4 ml-[auto] sm:ml-0">
      <button
        v-for="(value, index) in typeOfSkill"
        :key="index"
        class="px-4 py-3 selector-bg-hover left-border-one text-left text-lg sm:border-l-2 sm:border-b-0 border-l-0 border-b-2 transition ease-in-out delay-100 translate font-bold"
        @click="selectTechnology(index)"
        :class="
          selectedTech === value
            ? 'left-border-two sm:border-l-3 sm:border-b-0 border-l-0 border-b-3'
            : null
        "
      >
        {{ value }}
      </button>
    </div>

    <!-- Tech navigation-->
    <div class="mt-5 lg:-mt-5 lg:pt-0">
      <div
        v-for="(skills, index) in skillData"
        :key="index"
        class="flex flex-row sm:flex-col"
      >
        <div
          v-if="skills.type === selectedTech"
          class="flex sm:flex-row flex-col gap-2 lg:gap-8 ml-0 sm:ml-4 animate__animated animate__fadeIn"
        >
          <div class="grid lg:grid-cols-4 sm:grid-cols-3 grid-cols-2">
            <CardComponent
              v-for="(tech, techIndex) in skills.technologies"
              :key="techIndex"
              @click="selectedLang = tech.title"
              class="px-2 sm:px-5 py-2 left-border-one transition ease-in-out delay-100 flex"
              :class="selectedLang === tech.title ? 'left-border-two' : null"
              :title="tech.title"
              :image="tech.image"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Skills from './MainSkillsContent.json';
import CardComponent from './CardComponent.vue';

const skillData = Skills;
const typeOfSkill = ['Фронтенд', 'Бэкенд', 'Дизайн'];

const selectedTech = ref('');
const selectedLang = ref('');

function selectTechnology(index) {
	switch (index) {
	case 0:
		selectedTech.value = 'Фронтенд';
		break;
	case 1:
		selectedTech.value = 'Бэкенд';
		break;
	case 2:
		selectedTech.value = 'Дизайн';
		break;
	}
	setDefaultSelectLang(index);
}

function setDefaultSelectLang(index) {
	const tech = skillData[index]?.technologies?.[0]?.title;
	if (tech) selectedLang.value = tech;
}

onMounted(() => {
	selectTechnology(0);
});
</script>

<style>
  .selector-bg-hover:hover {
    background-color: var(--bg-sel);
  }

  .left-border-one {
    border-color: var(--text-highlight);
  }

  .left-border-two {
    border-color: var(--text-highlight-2) !important;
  }

  .div-right {
    right: 0;
    margin-left: auto;
    margin-right: 0;
    float: right;
  }
</style>
