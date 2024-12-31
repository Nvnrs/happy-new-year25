<script setup>
import Rocket from "./Rocket.vue";
import { gsap } from "gsap";
import { ref, watch, defineEmits, onMounted } from "vue";

const number_of_click = 3;
const click = ref(0);

const emit = defineEmits(["finish_tl", "finish_animation"]);

// rockets
const rocket1 = ref();
const rocket2 = ref();
const rocket3 = ref();
const rockets = [rocket1, rocket2, rocket3];

// PULSE
const pulse1 = ref();
const pulse2 = ref();
const pulse3 = ref();
const pulse = [pulse1, pulse2, pulse3];

function animation(click) {
  if (click != 3) return false;
  const tl_rocket = gsap.timeline();

  rockets.forEach((rocket) => {
    rocket.value.main.style.transition = "0s";
  });

  tl_rocket.to(".rocket", {
    scale: 0.7,
    filter: "blur(1px)",
  });

  tl_rocket.to(".rocket", {
    scale: 1.1,
    stagger: 0.1,
  });

  tl_rocket.to(".rocket", {
    y: "-150vh",
    filter: "blur(15px)",
    stagger: 0.1,
    duration: 1,
  });

  gsap.to(".intro", {
    scale: 0,
    delay: 0.5,
    onComplete: () => emit("finish_tl"),
  });

  tl_rocket.eventCallback("onComplete", () => emit("finish_animation"));
}

function increment_click() {
  if (click.value != number_of_click) {
    const scale = click.value ? click.value * 2.2 : 1.2;
    pulse[click.value].value.style.transform = `scale(${scale})`;
    rockets[click.value].value.main.style.transition = "0.2s";
    rockets[click.value].value.main.style.bottom = "-5vh";
    click.value++;
    animation(click.value);
  } else {
  }
}

onMounted(() => {
  const interval = setInterval(() => {
    increment_click();
  }, 800);
});
</script>

<template>
  <div class="intro-page">
    <div class="page-padding">
      <div class="intro">
        <span class="intro__pulse pulse1" ref="pulse1"></span>
        <span class="intro__pulse pulse2" ref="pulse2"></span>
        <span class="intro__pulse pulse2" ref="pulse3"></span>
        <h1 class="h1__intro">{{ 3 - click }}</h1>
        <p class="text__intro">Prêts ?</p>
        <div class="finger">
          <div class="finger__svg"></div>
        </div>
      </div>
    </div>
    <Rocket class="first-rocket rocket" ref="rocket1"></Rocket>
    <Rocket class="second-rocket rocket" ref="rocket2"></Rocket>
    <Rocket class="third-rocket rocket" ref="rocket3"></Rocket>
  </div>
</template>

<style scoped>
.intro-page {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.intro-page .page-padding {
  display: flex;
  justify-content: center;
  align-items: center;
}

.intro {
  border-radius: 100%;
  height: 200px;
  width: 200px;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  background-color: orange;
  color: white;
}

.intro__pulse {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  border-radius: 110%;
  background-color: orange;
  transition: 0.3s;
}

.pulse1 {
  z-index: -1;
  opacity: 0.5;
}
.pulse2 {
  z-index: -2;
  opacity: 0.2;
}

.pulse3 {
  z-index: -2;
  opacity: 0.2;
}

.h1__intro {
  margin-bottom: 1rem;
  font-size: 4rem;
}

.finger {
  position: absolute;
  right: -60px;
  top: -80px;
}

.rocket-container {
  position: absolute;
  bottom: -5vh;
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.first-rocket {
  position: absolute;
  bottom: -20vh;
  left: -10vw;
  transform: rotate(20deg);
}

.third-rocket {
  position: absolute;
  bottom: -20vh;
  left: 0;
  right: 0;
  margin: auto;
}

.second-rocket {
  position: absolute;
  bottom: -20vh;
  right: -10vw;
  transform: rotate(-20deg);
}
</style>
