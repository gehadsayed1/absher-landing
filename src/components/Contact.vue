<script setup>
import { ref } from "vue";
import { useI18n } from "vue-i18n";
import emailjs from "emailjs-com";
import Swal from "sweetalert2"; 


const { t } = useI18n();


const contactForm = ref({
  firstName: "",
  lastName: "",
  email: "",
  message: ""
});


const contactInfoKeys = {
  address: t("address"),
  phone1: t("phone1"),
  phone2: t("phone2"),
  phone3: t("phone3"),
  email: t("email"),
  website: t("website")
};


const sendEmail = async () => {
  const serviceID = "service_9soot3a";
  const templateID = "template_scymzhe";
  const userID = "QR_yTc93M0JDJwxC-"; 

  try {
    await emailjs.send(serviceID, templateID, {
      firstName: contactForm.value.firstName,
      lastName: contactForm.value.lastName,
      from_email: contactForm.value.email,
      message: contactForm.value.message,
      to_email: "gehadsaed199@gmail.com"
    }, userID);
    Swal.fire({
      title:  t("emailSent") ,
      icon: "success",
      confirmButtonText: t("ok")
    });
  
    contactForm.value.firstName = "";
    contactForm.value.lastName = "";
    contactForm.value.email = "";
    contactForm.value.message = "";
  } catch (error) {
    Swal.fire({
      title: t("emailNotSent"),
      icon: "error",
      confirmButtonText: t("ok")
    });
    console.error(error);
  }
};
</script>

<template>
  <div class="untree_co-section bg-light" id="contact-section">
    <div class="container">
      <div class="row mb-4" data-aos="fade-up" data-aos-delay="0">
        <div class="col-12 text-center mb-5">
          <h2 class="heading">{{ t("heading") }}</h2>
          <p>{{ t("subHeading") }}</p>
        </div>
      </div>
      <div class="row">
        <div class="col-lg-7">
          <form class="contact-form" @submit.prevent="sendEmail" data-aos="fade-up" data-aos-delay="100">
            <div class="row">
              <div class="col-6">
                <div class="form-group">
                  <label for="fname">{{ t("firstName") }}</label>
                  <input type="text" class="form-control" id="fname" v-model="contactForm.firstName" required />
                </div>
              </div>
              <div class="col-6">
                <div class="form-group">
                  <label for="lname">{{ t("lastName") }}</label>
                  <input type="text" class="form-control" id="lname" v-model="contactForm.lastName" required />
                </div>
              </div>
            </div>
            <div class="form-group">
              <label for="email">{{ t("email") }}</label>
              <input type="email" class="form-control" id="email" v-model="contactForm.email" required />
            </div>
            <div class="form-group">
              <label for="message">{{ t("message") }}</label>
              <textarea class="form-control" id="message" v-model="contactForm.message" cols="30" rows="5"></textarea>
            </div>
            <button type="submit" class="butt" data-aos="fade-up">
              {{ t("buttonSendMessage") }}
            </button>
          </form>
        </div>
        <div class="col-lg-4 ml-auto contect-info" data-aos="fade-up" data-aos-delay="200">
          <h3 class="h5 mb-4">{{ t("contactInfoHeading") }}</h3>
          <address class="text-black d-flex">
            <span class="mt-1 icon-room mr-2"></span>
            <span>{{ contactInfoKeys.address }}</span>
          </address>
          <ul class="list-unstyled ul-links mb-4">
            <li>
              <a :href="'tel://' + contactInfoKeys.phone1" class="d-flex">
                <span class="mt-1 icon-phone mr-2"></span>
                <span>{{ contactInfoKeys.phone1 }}</span>
              </a>
            </li>
            <li v-if="contactInfoKeys.phone2">
              <a :href="'tel://' + contactInfoKeys.phone2" class="d-flex">
                <span class="mt-1 icon-phone mr-2"></span>
                <span>{{ contactInfoKeys.phone2 }}</span>
              </a>
            </li>
            <li v-if="contactInfoKeys.phone3">
              <a :href="'tel://' + contactInfoKeys.phone3" class="d-flex">
                <span class="mt-1 icon-phone mr-2"></span>
                <span>{{ contactInfoKeys.phone3 }}</span>
              </a>
            </li>
            <li>
              <a :href="'mailto:' + contactInfoKeys.email" class="d-flex">
                <span class="mt-1 icon-envelope mr-2"></span>
                <span>{{ t("emailAddress") }}</span>
              </a>
            </li>
            <li v-if="contactInfoKeys.website && contactInfoKeys.website !== '#'">
              <a :href="contactInfoKeys.website" target="_blank" class="d-flex">
                <span class="mt-1 icon-globe mr-2"></span>
                <span>{{ contactInfoKeys.website }}</span>
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.untree_co-section {
  padding: 50px 0;
  position: relative;
  background-color: #eee;
}
@media (max-width: 991.98px) {
  .untree_co-section {
    padding: 50px 0;
  }
}
.untree_co-section .heading {
  font-size: 38px;
  color: #000000;
}
.untree_co-section .heading strong {
  font-weight: 700;
}
.untree_co-section .caption {
  color: #407BFF;
  font-size: 13px;
  text-transform: uppercase;
  font-weight: 700;
  display: inline-block;
}
.form-control {
  border: none;
  font-size: 16px;
  height: 45px;
  padding-left: 0;
  padding-right: 0;
  background: transparent;
  border-bottom: 1px solid #43434d;
  border-radius: 0;
  color: #000000;
}
.form-control:active,
.form-control:focus {
  color: #000000;
  border-color: #407BFF;
  -webkit-box-shadow: none;
  box-shadow: none;
  background: transparent;
}
.list-unstyled li a {
  color: #000000;
  margin-bottom: 8px;
}
.butt {
  background-color: var(--primary-color);
  color: #fff;
  padding: 8px 20px;
  border: 1px solid var(--primary-color);
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.3s ease-in-out;
}
@media (max-width: 767px) {
  .contect-info {
    margin-top: 40px;
  }
  @media (max-width: 991.98px) {
    .untree_co-section .heading {
      font-size: 28px;
    }
  }
}
</style>
