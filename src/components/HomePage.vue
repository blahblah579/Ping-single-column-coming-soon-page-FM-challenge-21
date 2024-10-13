<template>
  <v-container>
    <v-row class="d-flex flex-column">
      <v-col cols="12" class="d-flex justify-center mt-16">
        <div>
          <img class="img1" src="/src/assets/logo.svg" alt="Logo" />
        </div>
      </v-col>

      <v-col cols="12" class="text-center">
        <div class="heading">
          We are launching <span class="soon">soon!</span>
        </div>
        <div class="subheading">Subscribe and get notified</div>
      </v-col>

      <!-- Email Input Field with capsule border and Subscribe Button aligned to the right -->
      <v-col
        v-if="!isScreenLarge"
        cols="12"
        class="mt-2 mb-13 d-flex flex-column align-center justify-center"
      >
        <form
          class="form-row d-flex flex-column align-center"
          @submit.prevent="submit"
        >
          <div :class="['input-container', { 'error-border': errorMessage }]">
            <input
              v-model="email"
              type="text"
              placeholder="Your email address..."
              class="email-input ml-3"
              required
            />
          </div>
          <!-- <v-col cols="12" class="msg mt-1 pl-10 pa-0">{{ errorMessage }}</v-col> -->
          <div class="msg">{{ errorMessage }}</div>
        </form>

        <v-btn
          @click="submit"
          class="text-capitalize subscribe-btn d-flex justify-center align-center"
        >
          Notify Me
        </v-btn>
      </v-col>

      <!-- Email Input Field with capsule border and Subscribe Button aligned to the right -->
      <v-col
        v-else
        cols="12"
        class="mt-2 mb-13 d-flex flex-column justify-center align-center"
      >
        <form
          class="form-row d-flex flex-column flex-sm-row justify-center align-center"
          @submit.prevent="submit"
        >
          <div
            :class="[
              'input-container d-flex flex-column',
              { 'error-border': errorMessage },
            ]"
          >
            <input
              v-model="email"
              type="text"
              placeholder="Your email address..."
              class="email-input ml-3"
              required
            />
          </div>
          <v-btn
            @click="submit"
            class="ml-5 py-6 px-10 text-capitalize subscribe-btn d-flex justify-center align-center"
          >
            Notify Me
          </v-btn>
        </form>
        <div class="msg">{{ errorMessage }}</div>
      </v-col>

      <v-col cols="12">
        <div class="d-flex justify-center">
          <img
            class="img2"
            src="/src/assets/illustration-dashboard.png"
            alt="Illustration"
          />
        </div>
      </v-col>

      <v-col cols="12" class="mt-10 pb-0 icons d-flex justify-center">
        <!-- Social media icons with hover effects -->
        <div class="icon-container fb d-flex justify-center align-center">
          <v-avatar class="icon-avatar">
            <v-icon icon="mdi-facebook" size="medium" class="icon"></v-icon>
          </v-avatar>
        </div>
        <div class="icon-container twitter d-flex justify-center align-center">
          <v-avatar class="icon-avatar">
            <v-icon icon="mdi-twitter" size="medium" class="icon"></v-icon>
          </v-avatar>
        </div>
        <div
          class="icon-container instagram d-flex justify-center align-center"
        >
          <v-avatar class="icon-avatar">
            <v-icon icon="mdi-instagram" size="medium" class="icon"></v-icon>
          </v-avatar>
        </div>
      </v-col>

      <v-col cols="12" class="cr pa-0 mb-10">
        <div class="tagline d-flex align-center justify-center">
          <v-icon class="cr-logo mr-1" icon="mdi-copyright"></v-icon>
          Copyright Ping. All rights reserved.
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const email = ref("");
const errorMessage = ref(""); // Message for email validation errors
const isScreenLarge = ref(window.innerWidth >= 600); // Initialize variable

// Function to check screen size
const checkScreenSize = () => {
  isScreenLarge.value = window.innerWidth >= 600; // Update the variable based on window width
};

// Email validation and submission handler
const submit = () => {
  // Email pattern to include only .co or .com at the end
  const emailPattern = /^[^\s@]+@[^\s@]+\.(co|com)$/;

  if (emailPattern.test(email.value)) {
    errorMessage.value = ""; // Clear error message if email is valid
    alert(`Subscribed successfully with ${email.value}!!!`);
    email.value = ""; // Reset email field after submission
  } else {
    // Display appropriate error message
    errorMessage.value = "Please provide a valid email address";
  }
};

// Set up event listeners for window resize
onMounted(() => {
  window.addEventListener("resize", checkScreenSize);
});

// Clean up event listeners on component unmount
onBeforeUnmount(() => {
  window.removeEventListener("resize", checkScreenSize);
});
</script>

<style scoped>
@font-face {
  font-family: f1;
  src: url(/src/assets/LibreFranklin-Light.ttf);
}
@font-face {
  font-family: f2;
  src: url(/src/assets/LibreFranklin-Bold.ttf);
}
@font-face {
  font-family: f3;
  src: url(/src/assets/LibreFranklin-MediumItalic.ttf);
}

.img1 {
  width: 90%;
}
.img2 {
  width: 48%;
}
.heading {
  font-size: 42px;
  font-family: f1;
  color: hsl(0, 0%, 50%);
}
.soon {
  font-family: f2;
  color: black;
}
.subheading {
  color: hsl(210, 6%, 20%);
  font-size: 20px;
  font-family: f1;
  letter-spacing: -0.5px;
}

/* Input container - capsule shape with red border */
.input-container {
  display: flex;
  align-items: center;
  border: 1.5px solid hsl(216, 32%, 91%); /* Red border */
  border-radius: 25px; /* Capsule shape */
  padding-left: 10px;
  padding-right: 0; /* No right padding for button alignment */
  width: 62%;
  max-width: 600px;
  height: 50px;
}

/* Email input field inside capsule with transparent background and black text */
.email-input {
  width: 100%;
  height: 100%;
  border: none;
  outline: none;
  background-color: transparent;
  color: black;
  font-size: 16px;
}

/* Ensure no background color appears when input is focused */
.email-input:focus {
  outline: none;
  background-color: transparent;
}

/* Subscribe button aligned to the right */
.subscribe-btn {
  border: none;
  height: 100%;
  border-radius: 25px;
  background-color: #4d7bf3;
  color: white;
  cursor: pointer;
  font-size: 16px;
  letter-spacing: 0px;
}

.subscribe-btn:hover {
  background-color: hsl(224, 87%, 70%);
}

/* Align email field and button in one row */
.form-row {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
}

.tagline {
  text-align: center;
  margin-top: 20px;
}

/* Error message styling */
.msg {
  font-size: 11px;
  color: hsl(351, 68%, 72%);
  margin-right: 300px;
  font-family: f3;
}

/* Social media icons - default white background, grey border, blue icons */
.icon-container {
  margin: 0 5px;
  border: 1.3px solid hsla(0, 0%, 59%, 30%); /* Grey border */
  border-radius: 50%;
  background-color: white;
  transition: background-color 0.3s ease, color 0.3s ease,
    border-color 0.3s ease;
  width: 30px;
  height: 30px;
}
.icon {
  color: hsl(221, 70%, 54%); /* Blue icon */
}

/* Hover effect - background turns blue, icon becomes white, border disappears */
.icon-container:hover {
  background-color: hsl(221, 70%, 54%);
  border-color: transparent;
}
.icon-container:hover .icon {
  color: white;
}

.fb,
.twitter,
.instagram {
  background: #fff;
  border-radius: 50%; /* Keep the border circular */
  border: 1.5px solid hsla(0, 0%, 59%, 10%); /* Light grey border */
  padding: 4px; /* Reduce the padding */
  display: inline-block;
  transition: background-color 0.3s ease, color 0.3s ease, border 0.3s ease;
}
.cr {
  color: hsl(0, 0%, 59%);
  font-size: 11px;
  opacity: 60%;
}
.cr-logo {
  color: hsl(0, 0%, 59%);
  font-size: 11px;
  opacity: 60%;
}
.error-border {
  border-color: hsl(351, 68%, 72%); /* Red color for error state */
}
@media (max-width: 599.5px) {
  .subscribe-btn {
    margin-top: 30px;
  }
  .img2 {
    width: 90%;
    margin-bottom: 80px;
  }
  .heading {
    margin-top: 20px;
    margin-bottom: 20px;
    font-size: 32px;
  }
  .soon {
    font-family: f2;
    color: black;
  }
  .subheading {
    font-size: 16px;
    letter-spacing: -0.5px;
  }
  .form-row {
    width: 130%;
    max-width: 1000px;
    margin: 0 0;
  }
  .msg {
    margin-right: 130px;
  }
  .subscribe-btn {
    letter-spacing: 0px;
    padding-left: 150px;
    padding-right: 150px;
    padding-top: 25px;
    padding-bottom: 25px;
  }
}
</style>
