<script setup>
import { onMounted, ref } from "vue";
import { gsap } from "gsap";
import { Fireworks } from "fireworks-js";

const bg = ref();
const number = ref(0);
const glow = ref("");

onMounted(() => {
  gsap.to(".new-page", {
    duration: 1,
    background: "linear-gradient(180deg, #19192c 20%, #745149 100%)",
    zIndex: 1,
  });

  gsap.to(".sky__new-page", {
    duration: 1,
    opacity: 1,
    scale: 1.2,
  });

  gsap.to(".bottom__new ", {
    duration: 1,
    delay: 0.5,
    scale: 1,
  });

  const fireworks = new Fireworks(bg.value, {
    /* options */
    gravity: 1,
    intensity: 15,
  });
  fireworks.start();

  let counter = 0;
  const intervalId = setInterval(() => {
    if (number.value === 9) {
      number.value = 0;
    }
    number.value++;
    counter++;

    if (counter > 10 && number.value == 5) {
      clearInterval(intervalId);
      glow.value = "glow";
    }
  }, 100);

  gsap.from(".number__new", {
    opacity: 0,
    duration: 2,
    y: 100,
  });

  gsap.to(".number__new", {
    fontSize: "5rem",
    duration: 1,
    delay: 2,
  });

  gsap.to(".h1__new", {
    opacity: 1,
    delay: 2,
  });
});
</script>
<template>
  <div class="new-page">
    <div class="background" ref="bg"></div>
    <div class="sky__new-page">
      <img src="/stars.png" alt="" />
    </div>
    <div class="page-padding">
      <div class="new-component">
        <div class="top__new"></div>
        <div class="mid__new">
          <h1 class="h1__new">BONNE ANNEE</h1>
          <h1 :class="`number__new selection ${glow}`">202{{ number }}</h1>
        </div>
        <div class="bottom__new glass">
          <p class="credit">@nvnrs</p>
          <a href="https://www.linkedin.com/in/nicolas-venerosy-0522bb23b/" class="item">
            <svg
              width="100%"
              height="100%"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M19 3C19.5304 3 20.0391 3.21071 20.4142 3.58579C20.7893 3.96086 21 4.46957 21 5V19C21 19.5304 20.7893 20.0391 20.4142 20.4142C20.0391 20.7893 19.5304 21 19 21H5C4.46957 21 3.96086 20.7893 3.58579 20.4142C3.21071 20.0391 3 19.5304 3 19V5C3 4.46957 3.21071 3.96086 3.58579 3.58579C3.96086 3.21071 4.46957 3 5 3H19ZM18.5 18.5V13.2C18.5 12.3354 18.1565 11.5062 17.5452 10.8948C16.9338 10.2835 16.1046 9.94 15.24 9.94C14.39 9.94 13.4 10.46 12.92 11.24V10.13H10.13V18.5H12.92V13.57C12.92 12.8 13.54 12.17 14.31 12.17C14.6813 12.17 15.0374 12.3175 15.2999 12.5801C15.5625 12.8426 15.71 13.1987 15.71 13.57V18.5H18.5ZM6.88 8.56C7.32556 8.56 7.75288 8.383 8.06794 8.06794C8.383 7.75288 8.56 7.32556 8.56 6.88C8.56 5.95 7.81 5.19 6.88 5.19C6.43178 5.19 6.00193 5.36805 5.68499 5.68499C5.36805 6.00193 5.19 6.43178 5.19 6.88C5.19 7.81 5.95 8.56 6.88 8.56ZM8.27 18.5V10.13H5.5V18.5H8.27Z"
                fill="currentColor"
              />
            </svg>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.new-page {
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  align-items: center;
  z-index: -1;
}

.background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.8;
}

.sky__new-page {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 15vh;
  z-index: -1;
  opacity: 0;
  animation: flash 5s linear infinite;
}

@keyframes flash {
  0% {
    opacity: 0.5;
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0.5;
  }
}

.sky__new-page img {
  object-fit: cover;
  width: 100%;
  height: 100%;
  opacity: 0.6;
}

.new-component {
  /* background: rgba(255, 255, 255, 0.053); */
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.mid__new {
  flex: 1;
  max-height: 60vh;
  max-width: 500px;
  margin: auto;
  font-size: 1.9rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #eccfbb;
  text-align: center;
}

.h1__new {
  opacity: 0;
  font-size: 5rem;
}

.number__new {
  color: rgb(255, 184, 51);
  font-size: 7.5rem;
  opacity: 1;
}

.glow {
  color: white;
  animation: glowAnimation 2s ease-in-out infinite alternate;
  transition: color 1s ease-in-out, text-shadow 1s ease-in-out; /* Transition fluide de la couleur et de la lueur */
}

@keyframes glowAnimation {
  0% {
    text-shadow: 0 0 5px #ffffff, 0 0 10px #ffffff, 0 0 15px #ffffff, 0 0 20px #ff4500,
      0 0 30px #ff4500;
  }
  100% {
    text-shadow: 0 0 5px #ffcc00, 0 0 10px #ffcc00, 0 0 15px #ffcc00, 0 0 20px #ff4500,
      0 0 30px #ff4500;
  }
}

.glass {
  background-color: rgba(255, 255, 255, 0.068);
  border-radius: 1rem;
  width: 100%;
  padding: 0.3rem 2rem;
  backdrop-filter: blur(100px);
  border: solid 2px;
  border-color: rgba(255, 255, 255, 0.037);
}

.bottom__new {
  transform: scaleX(0);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.item {
  width: 50px;
  height: 50px;
  padding: 0.5rem;
  background-color: #0e76a8;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  border-radius: 100%;
  transition: 0.2s;
  display: inline-block;
}

.item:hover {
  scale: 1.2;
}

.credit {
  font-size: 1rem;
  font-family: Arial, Helvetica, sans-serif;
  color: rgba(255, 255, 255, 0.663);
  font-style: italic;
}
</style>
