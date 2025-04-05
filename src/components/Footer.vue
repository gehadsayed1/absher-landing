<script setup>
import { useI18n } from "vue-i18n";
import { contactInfo } from "../data/items";

const { t } = useI18n();

const socialItems = [
  { link: "https://www.instagram.com/", icon: "icon-instagram" },
  { link: "https://www.twitter.com/", icon: "icon-twitter" },
  { link: "https://www.facebook.com/", icon: "icon-facebook" },
  { link: "https://www.linkedin.com/", icon: "icon-linkedin" },
  { link: "https://www.pinterest.com/", icon: "icon-pinterest" },
];
</script>

<template>
  <div class="site-footer">
    <div class="footer-dots"></div>
    <div class="container">
      <div class="row">
        <div class="col-lg-4">
          <div class="widget">
            <h3>{{ t("column1Heading") }}</h3>
            <p>{{ t("column1Text") }}</p>
          </div>
          <div class="widget">
            <h3>{{ t("connectHeading") }}</h3>
            <ul class="list-unstyled social">
              <li style="margin-right: 4px">
                <a :href="socialItems[0].link">
                  <span :class="socialItems[0].icon"></span>
                </a>
              </li>
              <li style="margin-right: 4px">
                <a :href="socialItems[1].link">
                  <span :class="socialItems[1].icon"></span>
                </a>
              </li>
              <li style="margin-right: 4px">
                <a :href="socialItems[2].link">
                  <span :class="socialItems[2].icon"></span>
                </a>
              </li>
              <li style="margin-right: 4px">
                <a :href="socialItems[3].link">
                  <span :class="socialItems[3].icon"></span>
                </a>
              </li>
              <li>
                <a :href="socialItems[4].link" class="pepal">
                  <span :class="socialItems[4].icon"></span>
                </a>
              </li>
            </ul>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="widget">
            <h3>{{ t("column4Heading") }}</h3>
            <address>{{ contactInfo.address }}</address>
            <ul class="list-unstyled links mb-4">
              <li>
                <a :href="'tel://' + contactInfo.phone1">
                  {{ contactInfo.phone1 }}
                </a>
              </li>
              <li>
                <a :href="'tel://' + contactInfo.phone2">
                  {{ contactInfo.phone2 }}
                </a>
              </li>
              <li>
                <a :href="'mailto:' + contactInfo.email">
                  <span>{{ contactInfo.email }}</span>
                </a>
              </li>
            </ul>
          </div>
        </div>

        <div class="col-lg-4">
          <h3 class="mb-4">{{ t("mapHeading") }}</h3>
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3608.3842451008372!2d55.33611372584396!3d25.257656529251538!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3e5f5ce923dd170f%3A0xe05fb3a7f45e0b08!2sGolden%20Business%20Center!5e0!3m2!1sar!2seg!4v1740073430240!5m2!1sar!2seg"
            width="300"
            height="250"
            style="border: 0"
            allowfullscreen=""
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade"
          ></iframe>
        </div>
      </div>

      <div class="row">
        <div class="col-12 mt-5 text-center">
          <p>
            {{ t("copyrightText") }}
            <span class="text-primary">ABSHER BELKHAIR</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.site-footer {
  background: #efefef;
  font-size: 14px;
  color: #888;
  padding: 70px 0 0 0;
}
.site-footer a {
  color: #407bff;
  position: relative;
  display: inline-block;
}
.site-footer .btn:before {
  display: none;
}
.site-footer .widget {
  margin-bottom: 40px;
  display: block;
  position: relative;
  z-index: 1;
}
.site-footer .widget h3 {
  font-size: 16px;
  color: #000000;
  margin-bottom: 30px;
}
.site-footer .widget .links {
  width: 150px;
}
.site-footer .widget .links li {
  margin-bottom: 10px;
}
.site-footer .widget .links li a {
  color: #777;
}
.site-footer .social li {
  display: inline-block;
}
.site-footer .social li a {
  display: inline-block;
  width: 30px;
  height: 30px;
  position: relative;
  background: #777;
  border-radius: 50%;
  color: #ffffff;
}
.site-footer .social li a:before {
  display: none;
}
.site-footer .social li a > span {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}
.site-footer .social li a:hover {
  background: #06007a;
  color: #ffffff;
}
</style>
