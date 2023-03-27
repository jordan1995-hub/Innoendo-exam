<template>
  <q-page class="flex flex-center">
    <div>
      <h2 class="">Card Counting</h2>
      <h5>Count: {{ count }} {{ decision }}</h5>

      <div class="row">
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card 2" @click="addCard(2)" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card 3" @click="addCard(3)" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card 4" @click="addCard(4)" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card 5" @click="addCard(5)" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card 6" @click="addCard(6)" />
    </div>

    <div class="col">
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card 7" @click="addCard(7)" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card 8" @click="addCard(8)" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card 9" @click="addCard(9)" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card 10" @click="addCard(10)" />
    </div>

    <di class="col">
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card J" @click="addCard('J')" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card Q" @click="addCard('Q')" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card K" @click="addCard('K')" />
      <q-btn class="q-ml-md q-mt-md" color="primary" label="Card A" @click="addCard('A')" />
    </di>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      count: 0,
      decision: 'Hold'
    }
  },
  methods: {
  addCard(card) {
    if (card >= 2 && card <= 6) {
      this.count++;
    }
    else if( card >= 7 && card <= 9){
      this.count-=5

      }else if (card >= 10 || card === 'J' || card === 'Q' || card === 'K' || card === 'A') {
      this.count--;
    } else {

    }

    if (this.count > 0) {
      this.decision = 'Bet';
    } else {
      this.decision = 'Hold';
    }
  }
}
  // methods: {
  //   addCard (card) {
  //     switch (card) {
  //       case 2:
  //       case 3:
  //       case 4:
  //       case 5:
  //       case 6:
  //         this.count++
  //         break
  //       case 7:
  //       case 8:
  //       case 9:
  //         this.count('hold')
  //         break
  //       case 10:
  //       case 'J':
  //       case 'Q':
  //       case 'K':
  //       case 'A':
  //         this.count--
  //         break
  //     }
  //     this.decision = this.count > 0 ? 'Bet' : 'Hold'
  //   }
  // }
}
</script>
