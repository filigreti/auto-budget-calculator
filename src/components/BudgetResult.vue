<template>
  <div v-if="show == true" class="budget-result">
    <div class="image-area">
      <img
        v-if="store.income < 100000"
        src="https://i.pinimg.com/564x/de/4a/15/de4a15f0c6dc1cb965dd514631d101d8.jpg"
        alt
        class="img-fluid"
      />
      <img
        v-if="store.income < 500000 && store.income > 100000"
        src="https://i.pinimg.com/564x/de/5c/a6/de5ca63b5f008b9b31c36281b2b655ad.jpg"
        alt
        class="img-fluid"
      />
      <img
        v-if="store.income > 500000"
        src="https://i.pinimg.com/564x/90/d8/5b/90d85b2967bee0a7001662449040b66d.jpg"
        alt
        class="img-fluid"
      />
    </div>
    <ul style="list-style:none">
      <li>Income: N{{store.income}}</li>
      <li>Age:{{store.age}} Years</li>
      <li>Gender:{{store.gender}}</li>
      <li>Status:{{store.status}}</li>
      <li v-if="store.dependants == 1">Dependant:{{store.dependants}}</li>
      <li v-else>Dependants:{{store.dependants}}</li>
    </ul>
    <div class="fifty-box">
      <div>
        <p>Housing</p>
        <p>Food</p>
        <p>Transportation</p>
        <p>Basic Utilities</p>
        <p>Personal</p>
        <p>Travel</p>
        <p>Entertainment</p>
        <p>Monthly subscriptions.</p>
        <p>Meals out</p>
        <p>Paying off debt</p>
      </div>
      <div>
        <p>{{randomTen[0]}}%</p>
        <p>{{randomTen[1]}}%</p>
        <p>{{randomTen[2]}}%</p>
        <p>{{randomTen[3]}}%</p>
        <p>{{randomTen[4]}}%</p>
        <p>{{randomTen[5]}}%</p>
        <p>{{randomTen[6]}}%</p>
        <p>{{randomTen[7]}}%</p>
        <p>{{randomTen[8]}}%</p>
        <p>{{randomTen[9]}}%</p>
      </div>
      <div>
        <p>N {{Math.round((randomTen[0]/100)* store.income)}}</p>
        <p>N {{Math.round((randomTen[1]/100)* store.income)}}</p>
        <p>N {{Math.round((randomTen[2]/100)* store.income)}}</p>
        <p>N {{Math.round((randomTen[3]/100)* store.income)}}</p>
        <p>N {{Math.round((randomTen[4]/100)* store.income)}}</p>
        <p>N {{Math.round((randomTen[5]/100)* store.income)}}</p>
        <p>N {{Math.round((randomTen[6]/100)* store.income)}}</p>
        <p>N {{Math.round((randomTen[7]/100)* store.income)}}</p>
        <p>N {{Math.round((randomTen[8]/100)* store.income)}}</p>
        <p>N {{Math.round((randomTen[9]/100)* store.income)}}</p>
      </div>
    </div>
    <div class="footer-back">
      <i @click="goBack" class="far fa-arrow-alt-circle-left icon-left"></i>
      <span>Go Back</span>
    </div>
  </div>
  <div v-else>
    <carousel
      :per-page="1"
      :autoplay="true"
      :paginationEnabled="false"
      :loop="true"
      :autoplayTimeout="5000"
    >
      <slide v-for="(image,index) in fundImages" :key="index">
        <img :src="image" alt class="image-fluid" />
      </slide>
    </carousel>
  </div>
</template>

<script>
import { Carousel, Slide } from "vue-carousel";
export default {
  props: {
    store: Object,
    show: Boolean,
    reset: Function
  },
  components: {
    Carousel,
    Slide
  },
  data() {
    return {
      fundImages: [
        "https://buildinganest.co/wp-content/uploads/2017/10/14.png",
        "https://buildinganest.co/wp-content/uploads/2017/10/3-1.png",
        "https://buildinganest.co/wp-content/uploads/2017/10/7.png",
        "https://buildinganest.co/wp-content/uploads/2017/10/30.png"
      ],
      randomTen: []
    };
  },
  methods: {
    randombetween(min, max) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    },
    generate(max, thecount) {
      var r = [];
      var currsum = 0;
      for (var i = 0; i < thecount - 1; i++) {
        r[i] = this.randombetween(1, max - (thecount - i - 1) - currsum);
        currsum += r[i];
      }
      r[thecount - 1] = max - currsum;
      return r;
    },
    goBack() {
      this.reset();
    }
  },
  mounted() {
    this.randomTen = this.generate(100, 10);
  }
};
</script>

<style>
.image-fluid {
  width: 100%;
  height: 60vh;
  object-fit: contain;
  margin-top: 20px;
}
.fifty-box {
  display: flex;
  width: 83%;
  margin: auto;
  justify-content: space-between;
}
p {
  padding: 0;
  margin: 0;
  margin-bottom: 10px;
}
.budget-result {
  position: relative;
}
.image-area {
  position: absolute;
  right: 6vw;
  top: 2vh;
}
.img-fluid {
  width: 100px;
}
.icon-left {
  padding-left: 3vw;
  font-size: 30px;
}
.footer-back {
  display: flex;
  align-items: center;
  margin-top: 20px;
}
.footer-back span {
  padding-left: 5px;
}
</style>
