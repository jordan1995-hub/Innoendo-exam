<template>
  <q-page class="column items-center">
    <div class="q-mt-xl">
      <label for="price">Purchase Price:</label>
      <q-input outlined type="number"  v-model="price" id="price" step="0.01" label="Price" />
      <label for="cash">Cash:</label>
      <q-input outlined type="number"  v-model="cash" id="cash" step="0.01" label="cash" />
      <q-btn class="q-mt-lg q-ml-md" color="primary" label="Check cash Register"  @click="checkCashRegister" />
      <div  v-if="status !== null">
        <h6>Status: {{ status }}</h6>

        <ul>
          <div step="0.01" v-for="(amount, currency) in change" :key="currency">
            {{ currency }}: {{ amount }}
          </div>
        </ul>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
      price: null,
      cash: null,
      cid: [
        ["PENNY", 0],
        ["NICKEL", 0],
        ["DIME", 0],
        ["QUARTER", 0],
        ["ONE", 0],
        ["FIVE", 0],
        ["TEN", 0],
        ["TWENTY", 0],
        ["ONE HUNDRED", 0]
      ],
      status: null,
      change: {}
    };
  },
  methods: {
    checkCashRegister() {
      const currencyValues = {
        "ONE HUNDRED": 100,
        TWENTY: 20,
        TEN: 10,
        FIVE: 5,
        ONE: 1,
        QUARTER: 0.25,
        DIME: 0.1,
        NICKEL: 0.05,
        PENNY: 0.01
      };

      let totalCid = 0;
      for (let i = 0; i < this.cid.length; i++) {
        const currency = this.cid[i][0];
        const amount = this.cid[i][1];
        totalCid += amount;
        this.change[currency] = amount;
      }

      const changeDue = this.cash - this.price;

      if (changeDue > totalCid) {
        this.status = "INSUFFICIENT_FUNDS";
        this.change = [];
        return;
      }

      if (changeDue === totalCid) {
        this.status = "CLOSED";
        this.change = this.cid;
        return;
      }

      const changeToReturn = {};
      for (let i = this.cid.length - 1; i >= 0; i--) {
        const currency = this.cid[i][0];
        const currencyAmount = this.cid[i][1];
        const currencyValue = currencyValues[currency];
        let amountToReturn = 0;

        while (changeDue >= currencyValue && currencyAmount > 0) {
          changeDue -= currencyValue;
          changeDue = Math.round(changeDue * 100) / 100;
          currencyAmount -= currencyValue;
          amountToReturn += currencyValue;
        }

        if (amountToReturn > 0) {
          changeToReturn[currency] = amountToReturn;
          this.change[currency] -= amountToReturn;
        }
      }

      if (changeDue > 0) {
        this.status = "INSUFFICIENT_FUNDS";
        this.change = [];
        return;
      }

      this.status = "OPEN";
      this.change = changeToReturn;
    }
  }
}
</script>
