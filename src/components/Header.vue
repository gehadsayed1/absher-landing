<script setup>
import { siteName } from "../data/items";
import { useI18n } from "vue-i18n";
import { ref, onMounted } from "vue";
import flagEg from "../assets/images/eg.png";
import flagEn from "../assets/images/en.png";
import logo from "../assets/images/Subheading (3).png";

const { t, locale } = useI18n();
const selectedLanguage = ref(locale.value);
const isDropdownOpen = ref(false);

const selectLanguage = ref([
  { value: "en", label: "English", img: flagEn },
  { value: "ar", label: "العربية", img: flagEg },
]);

onMounted(() => {
  const savedLanguage = localStorage.getItem("language") || "en";
  selectedLanguage.value = savedLanguage;
  locale.value = savedLanguage;
  document.documentElement.dir = savedLanguage === "ar" ? "rtl" : "ltr";
});

const changeLanguage = (lang) => {
  selectedLanguage.value = lang.value;
  localStorage.setItem("language", lang.value);
  locale.value = lang.value;
  document.documentElement.dir = lang.value === "ar" ? "rtl" : "ltr";
  isDropdownOpen.value = false;
};

const isSidebarOpen = ref(false);

const toggleSidebar = () => {
  isSidebarOpen.value = !isSidebarOpen.value;
};
</script>

<template>
 
  <nav class="main-nav">
    <div class="container">
      <div class="nav-container">
       
        <div class="nav-logo">
          <a href="#home-section">
            <img :src="logo" alt="">
          </a>
        </div>    
        <div class="nav-right">      
          <div class="lang-selector">
            <div class="lang-dropdown" @click="isDropdownOpen = !isDropdownOpen">
              <img
                :src="selectLanguage.find(lang => lang.value === selectedLanguage)?.img"
                class="flag"
              />
              <span>
                {{ selectLanguage.find(lang => lang.value === selectedLanguage)?.label }}
              </span>
              <span class="arrow">&#9662;</span>
            </div>
            <ul v-if="isDropdownOpen" class="lang-options">
              <li v-for="lang in selectLanguage" :key="lang.value" @click="changeLanguage(lang)">
                <img :src="lang.img" class="flag" />
                <span>{{ lang.label }}</span>
              </li>
            </ul>
          </div>
        
          <ul class="main-menu">
            <li><a href="#home-section">{{ t("home") }}</a></li>
            <li><a href="#features-section">{{ t("features") }}</a></li>
            <li><a href="#about-section">{{ t("about") }}</a></li>
            <li><a href="#contact-section">{{ t("contact") }}</a></li>
          </ul>
        </div>
       
        <div class="burger-menu" @click="toggleSidebar">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    </div>
  </nav>

  <transition name="slide">
    <div v-if="isSidebarOpen" class="mobile-sidebar">
      <button class="close-icon" @click="toggleSidebar">×</button>
      <ul class="mobile-menu">
        <li>
          <a href="#home-section" @click="toggleSidebar">{{ t("home") }}</a>
        </li>
        <li>
          <a href="#features-section" @click="toggleSidebar">{{ t("features") }}</a>
        </li>
        <li>
          <a href="#about-section" @click="toggleSidebar">{{ t("about") }}</a>
        </li>
        <li>
          <a href="#contact-section" @click="toggleSidebar">{{ t("contact") }}</a>
        </li>
      </ul>
    </div>
  </transition>
</template>

<style scoped>

:global(html) {
  scroll-behavior: smooth;
}


* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}


.main-nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: #fff;
  padding: 10px 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}

.nav-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}


.nav-logo img{
width: 60px;
height: 50px;
}


.nav-right {
  display: flex;
  align-items: center;
}


.lang-selector {
  position: relative;
  margin-right: 20px;
}
.lang-dropdown {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 6px 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background: var(--primary-color);
  color: #fff;
  cursor: pointer;
  font-size: 14px;
}
.flag {
  width: 20px;
  height: 20px;
  object-fit: cover;
}
.arrow {
  font-size: 12px;
}
.lang-options {
  position: absolute;
  top: 110%;
  left: 0;
  background: #fff;
  border: 1px solid #ccc;
  border-radius: 5px;
  list-style: none;
  width: 100%;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  z-index: 100;
}
.lang-options li {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 10px;
  cursor: pointer;
  transition: background 0.2s;
}
.lang-options li:hover {
  background: #f0f0f0;
}


.main-menu {
  list-style: none;
  display: flex;
  gap: 20px;
}
.main-menu li a {
  text-decoration: none;
  color: #333;
  font-size: 16px;
  transition: color 0.2s;
}
.main-menu li a:hover {
  color: var(--primary-color, #007bff);
}


.burger-menu {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 21px;
  cursor: pointer;
}
.burger-menu span {
  display: block;
  height: 3px;
  background: #333;
  border-radius: 3px;
}

.mobile-sidebar {
  position: fixed;
  top: 70px;
  right: 0;
  width: 250px;
  height: 100%;
  background: #fff;
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.3);
  z-index: 200;
  padding: 20px;
  overflow-y: auto;
}
.mobile-menu {
  list-style: none;
  margin-top: 50px;
}
.mobile-menu li {
  margin-bottom: 20px;
}
.mobile-menu li a {
  text-decoration: none;
  color: #333;
  font-size: 18px;
}
.close-icon {
  position: absolute;
  top: 10px;
  right: 10px;
  background: transparent;
  border: none;
  font-size: 30px;
  cursor: pointer;
}
.close-icon:focus {
  outline: none;
}

.slide-enter-active,
.slide-leave-active {
  transition: transform 0.3s ease;
}
.slide-enter-from,
.slide-leave-to {
  transform: translateX(100%);
}


@media (max-width: 991px) {
  .burger-menu {
    display: flex;
  }
  .main-menu {
    display: none;
  }
}
</style>
