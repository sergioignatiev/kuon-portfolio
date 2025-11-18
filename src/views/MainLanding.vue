<template>
  <div class="flex flex-col gap-[2.5rem]">
    <!-- introduction section -->
    <div class="divCenter">
      <p
        id="landing_intro"
        ref="landingIntro"
        class="lg:text-xl text-md acrlyic w-auto text-center selector"
      ></p>
    </div>
    <section class="">
      <h1 class="text-4xl font-bold">Сергей Игнатьев</h1>
      <h3 class="text-lg">Фронтенд разработчик</h3>
    </section>
    <section class="pt-2">
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        Профессиональная информация
      </h2>
      <br />
      <p class="lg:text-lg text-sm text-justify leading-6">
        &nbsp;&nbsp;&nbsp;&nbsp; Профессиональный младший веб-разработчик,
        способный разрабатывать профессионально выглядящие и удобные для
        пользователя веб-сайты с нуля и писать
        <strong
          >оптимизированный по производительности, переиспользуемый и
          рефакторируемый код</strong
        >. Профессионально разработал 5 веб-приложений с использованием
        нескольких JavaScript фреймворков.
      </p>
      <br />
      <p class="lg:text-lg text-sm text-justify leading-6">
        <!-- &nbsp;&nbsp;&nbsp;&nbsp; -->
        Hungry for knowledge, collaborative individual and possess analytical
        skills. Enjoys problem solving and willing to adapt to changes in the
        industry to stay on top.
      </p>
    </section>
    <!-- info section -->
    <section class="">
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        Личная информация
      </h2>
      <br />
      <p class="lg:text-lg text-sm text-justify leading-6">
        &nbsp;&nbsp;&nbsp;&nbsp; Aaron has a strong passion on technology and
        computers. Outside of programmimg, Aaron has a hobby of collecting and
        engage with technology. He likes to tinker with his Arch Linux Operating
        System and enjoys collecting custom keyboards.
      </p>
    </section>
    <!-- journey section -->
    <section class="">
      <h2
        class="lg:text-2xl text-lg font-bold underline underline-offset-8 decoration-2"
      >
        Опыт
      </h2>
      <br />
      <div class="flex flex-col gap-2">
        <!-- year 2017 -->
        <p class="lg:text-lg text-sm text-justify">
          <strong>2021:</strong>
          &nbsp; Начал изучать программирование как хобби.
        </p>
        <!-- year 2020 -->
        <p class="lg:text-lg text-sm text-justify">
          <strong>2022:</strong>
          &nbsp; Выучил React и начал делать сайты на фрилансе
        </p>
        <!-- year 2022  -->
        <p class="lg:text-lg text-sm text-justify">
          <strong>2024:</strong>
          &nbsp; Начал работать с Vue и Nuxt.js, углубился в фронтенд разработку
          и сделал несколько коммерческих проектов.
        </p>
      </div>
    </section>
  </div>
</template>

<script>
import TypeIt from 'typeit';
import 'animate.css';
import { ref } from 'vue';

export default {
	data() {
		return {
			display: false
		};
	},
	setup() {
		const landingIntro = ref('');

		if (landingIntro.value !== '') {
			landingIntro.value === '';
		}
	},
	mounted() {
		new TypeIt('#landing_intro', {
			speed: 50,
			waitUntilVisible: true,
			startDelay: 2000,
			startDelete: true,
			// remove cursor when finished
			afterComplete: function (instance) {
				instance.destroy();
			}
		})
			.type('Приветствую.Я Фронтенд разработчик из Новороссийска.')
			.go();
	}
};
</script>

<style>
  .selector {
    background-color: var(--bg-sel);
  }

  .copyright {
    animation: fadeInLeft; /* referring directly to the animation's @keyframe declaration */
    animation-duration: 1s; /* don't forget to set a duration! */
    animation-delay: 3s;
  }

  /* @keyframes copyright {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
    visibility: visible;
  }
} */
</style>
