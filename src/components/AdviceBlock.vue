<template>
  <div class="wrapper">
    <div class="advice-container">
      <div class="advice-block">
        <h3 class="advice-title">Advice #{{ adviceId }}</h3>
        <p class="advice-quote">“{{ adviceQuote }}”</p>
        <img
          class="advice-img"
          src="../assets/images/pattern-divider-desktop.svg"
          alt="Pattern"
        />
        <img
          class="advice-img-mob"
          src="../assets/images/pattern-divider-mobile.svg"
          alt="Pattern"
        />
        <button @click="fetchAdvice" class="advice-btn">
          <img src="../assets/images/icon-dice.svg" alt="Dice" />
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { ref, onMounted } from "vue";
export default {
  setup() {
    const adviceId = ref();
    const adviceQuote = ref("");

    onMounted(() => {
      fetchAdvice();
    });

    // Getting data
    function fetchAdvice() {
      axios.get("https://api.adviceslip.com/advice").then((responce) => {
        adviceId.value = responce.data.slip.id;
        adviceQuote.value = responce.data.slip.advice;
      });
    }

    return {
      adviceId,
      adviceQuote,
      fetchAdvice,
    };
  },
};
</script>

<style scoped>
.advice-container {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.advice-block {
  display: flex;
  position: relative;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: hsl(217, 19%, 24%);
  border-radius: 15px;
  padding: 50px;
  max-width: 600px;
}
.advice-title {
  text-transform: uppercase;
  letter-spacing: 5px;
  font-size: 14px;
  color: hsl(150, 100%, 66%);
  padding-bottom: 30px;
}
.advice-quote {
  font-size: 28px;
  color: hsl(193, 38%, 86%);
  padding-bottom: 30px;
  text-align: center;
}
.advice-img {
  display: initial;
  padding-bottom: 20px;
}
.advice-img-mob {
  display: none;
  padding-bottom: 20px;
}
.advice-btn {
  display: flex;
  border: none;
  background: none;
  outline: none;
  cursor: pointer;
  position: absolute;
  bottom: -32px;

  background: hsl(150, 100%, 66%);
  padding: 20px;
  border-radius: 50px;
  transition: 0.4s ease;
}
.advice-btn:hover {
  box-shadow: 0 0 40px hsl(150, 100%, 66%);
  transition: 0.4s ease;
}
/* Responsive for mobile devices */
@media only screen and (max-width: 650px) {
  .advice-block {
    max-width: 350px;
  }
  .advice-img {
    display: none;
  }
  .advice-img-mob {
    display: initial;
  }
}
</style>
