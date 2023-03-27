<template>
  <q-page class="column items-center">

    <div class="col-auto q-mt-xl">
    <h1 class=" text-h2">Roman Numeral Converter</h1>
    </div>

    <div class="col-auto ">
    <q-form class="" @submit.prevent="convertToRoman">
      <q-input v-model="number" class="q-mt-md" type="number" label="Enter an number" dense outlined />
      <q-btn class="q-mt-md" type="submit" label="Convert to Roman Numeral" dense color="primary"
        :disable="number < 1 || number > 1000" />
    </q-form>
  </div>

    <div class="text-h5 q-mt-md" v-if="romanNumeral !== ''" >
      Roman Numeral Equivalent: {{ romanNumeral }}
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
      number: '',
      romanNumeral: ''
    }
  },
  methods: {
    convertToRoman() {
      const romanNumeralValues = [
        { value: 1000, symbol: 'M' },
        { value: 900, symbol: 'CM' },
        { value: 500, symbol: 'D' },
        { value: 400, symbol: 'CD' },
        { value: 100, symbol: 'C' },
        { value: 90, symbol: 'XC' },
        { value: 50, symbol: 'L' },
        { value: 40, symbol: 'XL' },
        { value: 10, symbol: 'X' },
        { value: 9, symbol: 'IX' },
        { value: 5, symbol: 'V' },
        { value: 4, symbol: 'IV' },
        { value: 1, symbol: 'I' },
      ];

      let romanNumeral = '';

      let num = parseInt(this.number);

      for (let i = 0; i < romanNumeralValues.length; i++) {
        while (num >= romanNumeralValues[i].value) {
          romanNumeral += romanNumeralValues[i].symbol;
          num -= romanNumeralValues[i].value;
        }
      }

      this.romanNumeral = romanNumeral;
    }
  }

}
</script>
