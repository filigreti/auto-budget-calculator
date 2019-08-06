<template>
  <div id="budget-card">
    <div class="card-one">
      <h3 class="text-center">Know your budget</h3>
      <form class="form-signin">
        <span class="currencyinput">
          <span class="currency">N</span>
          <input
            type="number"
            name="currency"
            required
            autofocus
            placeholder="Main Income"
            v-model.lazy="results.income"
            :disabled="visible == true"
          />
        </span>
        <span class="span-area">
          <select :disabled="visible == true" required v-model="results.age">
            <option value disabled selected>Age</option>
            <option
              v-for="n in Array.from({length: 53}, (x,i) => i + 18)"
              :value="n"
              :key="n"
            >{{ n }} yrs</option>
          </select>
        </span>
        <span class="span-area">
          <select :disabled="visible == true" required v-model="results.gender">
            <option value disabled selected>Gender</option>
            <option value="Male">Male</option>
            <option value="Female">Female</option>
          </select>
        </span>
        <span class="span-area">
          <select :disabled="visible == true" required v-model="results.status">
            <option value disabled selected>Marital Status</option>
            <option value="Married">Married</option>
            <option value="Single">Single</option>
            <option value="Divorced">Divorced</option>
            <option value="Widowed">Widowed</option>
          </select>
        </span>
        <span class="span-area">
          <select :disabled="visible == true" required v-model="results.dependants">
            <option value disabled selected>Dependants</option>
            <option
              v-for="n in Array.from({length: 15}, (x,i) => i + 1)"
              :value="n"
              :key="n"
            >{{ n }} Dependant(s)</option>
          </select>
        </span>
        <div v-if="visible == false" class="right">
          <button @click.prevent="next()" class="btn" type="submit" :disabled="validation">
            <i class="far fa-arrow-alt-circle-right icon-right"></i>
          </button>
        </div>
      </form>
    </div>
    <BudgetResult :store="results" :show="visible" class="card-two" :reset="resetData" />
  </div>
</template>

<script>
import BudgetResult from "./BudgetResult.vue";

export default {
  components: {
    BudgetResult
  },
  data() {
    return {
      results: {
        income: "",
        age: "",
        gender: "",
        status: "",
        dependants: ""
      },
      visible: false,
      validation: true
    };
  },
  watch: {
    results: {
      handler: function(item) {
        if (
          item.income != "" &&
          item.age != "" &&
          item.gender != "" &&
          item.status != "" &&
          item.dependants != ""
        ) {
          this.validation = false;
        } else {
          this.validation = true;
        }
      },
      deep: true
    }
  },
  methods: {
    next() {
      this.visible = true;
    },
    resetData() {
      Object.assign(this.$data, this.$options.data());
    }
  }
};
</script>

<style scoped>
#budget-card {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  width: 100%;
  height: 100%;
  z-index: 10;
}
#budget-card .card-one {
  width: 35vw;
  height: 70vh;
  background: white;
  opacity: 0.96;
  z-index: 10;
}
#budget-card .card-two {
  width: 35vw;
  height: 70vh;
  background: white;
  z-index: 10;
}
#budget-card .text-center {
  text-align: center;
}
#budget-card .form-signin {
  display: flex;
  flex-direction: column;
  width: 80%;
  margin: 35px auto;
}
#budget-card .email-label {
  font-size: 14px;
}
#budget-card .form-signin input {
  padding: 15px 4px;
  outline: none;
}
#budget-card .form-signin select {
  padding: 15px 4px;
  outline: none;

  border-radius: none;
  background: white;
}
.currencyinput {
  display: flex;
  align-items: center;
  border: 1px solid grey;
  /* border: 1px inset #ccc; */
  margin-bottom: 15px;
  position: relative;
}
.currencyinput input {
  border: 0;
  width: 85%;
}
.currency {
  padding-left: 10px;
  opacity: 0.5;
}
#budget-card select::-ms-expand {
  display: none;
}
#budget-card select {
  -webkit-appearance: none;
  -moz-appearance: none;
  text-indent: 20px;
  text-overflow: "";
  border: none;
  width: 100%;
}
#budget-card .span-area {
  border: 1px solid grey;
  margin-bottom: 15px;
}
#budget-card .right {
  display: flex;
  justify-content: flex-end;
  margin-top: 30px;
}
.icon-right {
  font-size: 40px;
}
.btn {
  border: none;
  outline: none;
}
</style>
