<script setup>
import Header from "./components/Header.vue";
import Hero from "./components/Hero.vue";
// import Service1 from "./components/Service1.vue";
import Service from "./components/Service.vue";
// import Service2 from "./components/Service2.vue";
// import Feature from "./components/Feature.vue";
// import Advantage from "./components/Advantage.vue";
import About from "./components/About.vue";
import Contact from "./components/Contact.vue";
import Footer from "./components/Footer.vue";

import { useI18n } from "vue-i18n";
import { watchEffect } from "vue";

const { locale } = useI18n();

watchEffect(() => {
  document.body.classList.toggle("rtl", locale.value === "ar");
  document.body.classList.toggle("ltr", locale.value === "en");
});
</script>

<template>
  <Header />
  <Hero />
  <!-- <Service1 /> -->
  <Service />
  <!-- <Service2 /> -->
  <!-- <Feature /> -->
  <!-- <Advantage /> -->
  <About />
  <Contact />
  <Footer />
</template>
