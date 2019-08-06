<template>
  <div id="app">
    <h1 class="nav animated fadeInRight delay-2s">
      <i class="fab fa-bitcoin bits"></i>
      <span class="logo-title">Auto-bit</span>
    </h1>
    <img :src="imageOne" alt class="chi-image" />

    <BudgetCard />
  </div>
</template>

<script>
import BudgetCard from "./components/BudgetCard.vue";

export default {
  name: "app",
  components: {
    BudgetCard
  },
  data() {
    return {
      imageOne:
        "https://i.pinimg.com/564x/4e/12/f6/4e12f609fd4a5f7cb476656f2c26f9ac.jpg",
      imageTwo:
        "https://i.pinimg.com/564x/03/ef/f4/03eff4cef27ee9d7545352845ac9741d.jpg"
    };
  }
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: "Roboto Condensed", sans-serif;
  background-image: linear-gradient(120deg, #fdfbfb 0%, #ebedee 100%);

  width: 100%;
  height: 100vh;
  position: relative;
}
.chi-image {
  width: 30vw;
  height: 60vh;
  position: absolute;
  left: 3vw;
  top: 3vh;
}
.nav {
  position: absolute;
  right: 6vw;
  color: #393534b9;
  padding: 5px;
  opacity: 0.1;
  font-size: 25px;
  display: flex;
  align-items: center;
}
.bits {
  font-size: 40px;
}
.logo-title {
  padding-left: 5px;
}
</style>
