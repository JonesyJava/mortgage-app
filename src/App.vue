<template>
  <div id="app">
    <header>
      <h1 class="text-center">
        <img
          src="https://raw.githubusercontent.com/trevorspielman/itt-mortgage-calculator-assignment/master/src/assets/logo.png"
          alt=""
          height="45"
        />
        Mortgage Calculator
      </h1>
    </header>
    <div class="row justify-content-center">
      <div class="col-6">
        <div class="form">
          <div class="form-group">
            <label><h5>Amount</h5></label>
            <input
              @input="this.calculateMortgage"
              v-model="state.amount"
              type="number"
              :step="1"
              class="form-control"
              placeholder=""
              aria-describedby="helpId"
            />
          </div>
        </div>
        <div class="form">
          <div class="form-group">
            <label><h5>Interest Rate</h5></label>
            <input
              @input="this.calculateMortgage"
              v-model="state.interest"
              type="number"
              class="form-control"
              placeholder=""
              aria-describedby="helpId"
            />
          </div>
        </div>
        <div class="form">
          <div class="form-group">
            <label><h5>Term</h5></label>
            <select
              @input="this.calculateMortgage"
              v-model="state.term"
              type="drop-down"
              class="form-control"
              placeholder=""
              aria-describedby="helpId"
            >
              <option>15</option>
              <option>30</option>
            </select>
          </div>
        </div>
        <div class="text-center">
          <h1>Total Balance</h1>
          <span>
            <h5>{{ state.balance }}</h5>
          </span>
        </div>
        <div class="text-center">
          <h1>Monthly Payment</h1>
          <span>
            <h5>{{ state.pmt }}</h5>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue'
import { calculate } from './Calculate.js'
import { logger } from './utils/Logger.js'
export default {
  name: 'App',
  setup() {
    const state = reactive({
      amount: 70000,
      interest: 5.5,
      term: 15,
      balance: 0,
      pmt: 0
    })
    // onMounted(() => this.calculateMortgage())
    return {
      state
    }
  },
  calculateMortgage() {
    logger.log(this.state)
    const res = calculate(this.state.amount, this.state.interest, this.state.term)
    logger.log(res)
    this.state.balance = res.balance
    this.state.pmt = res.pmt
  }
}

</script>
<style lang="scss">
@import "./assets/scss/main.scss";
</style>
