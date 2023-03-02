<script setup lang="ts">
import { ref, reactive, computed, watch, toRefs, onMounted, onBeforeMount, onUpdated } from 'vue'

//const itemName1 = ref<string>('Desk')
const itemName2 = 'Bike'

const item1 = reactive({
  name: 'Desk',
  price: 40000
})

//const price1 = 40000
const price2 = 20000

const url1 = 'https://www.amazon.com/'

const buy = (itemName: string) => {
  alert('Are you sure to buy ' + itemName + '?')
}

const input = (event: any) => {
  console.log('event.target.value:', event.target.value)
  item1.name = event.target.value
}

const inputPrice = (event: any) => {
  console.log('event.target.value:', event.target.value)
  item1.price = event.target.value
}

const clear = () => {
  item1.name = ''
  item1.price = 0
}

const budget = 50000

// const priceLabel = computed(() => {
//   return item1.price > budget ? 'too expensive' : item1.price + ' yen'
//   // if (item1.price > budget) {
//   //   return 'too expensive'
//   // } else {
//   //   return item1.price + ' yen'
//   // }
// })

const getPriceLabel = () => {
  if (item1.price > budget * 2) {
    return 'too expensive'
  } else if (item1.price > budget) {
    return 'expensive'
  } else {
    return item1.price + ' yen'
  }
}

onBeforeMount(() => {
  console.log('before mount')
})

onMounted(() => {
  console.log('mounted')
})

onUpdated(() => {
  console.log('update')
})

const priceLabel = ref<string>(item1.price + ' yen')
const { price } = toRefs(item1)
watch(price, () => {
  console.log('watch')
  if (price.value > budget * 2) {
    priceLabel.value = 'too expensive'
  } else if (price.value > budget) {
    priceLabel.value = 'expensive'
  } else {
    priceLabel.value = price.value + ' yen'
  }
})

</script>

<template>
  <div class="container">
    <h1>Payment</h1>
    <input v-model="item1.name" />
    <!-- <input v-on:input="input" v-bind:value="item1.name" /> -->
    <input v-model="item1.price" />
    <!-- <input v-on:input="inputPrice" v-bind:value="item1.price" /> -->
    <button v-on:click="clear">Clear</button>
    <div class="payment">
      <label>{{ item1.name }}</label>
      <!-- <label>{{ priceLabel }}</label> -->
      <label>{{ getPriceLabel() }}</label>
      <!-- <label>{{ item1.price > budget ? 'too expensive...' : item1.price + 'yen' }}</label> -->
      <!-- <label>{{ item1.price }} yen</label> -->
      <a v-bind:href="url1">bought at...</a>
      <button v-on:click="buy(item1.name)">BUY</button>
    </div>
    <div class="payment">
      <label>{{ itemName2 }}</label>
      <label>{{ price2 }} yen</label>
      <button v-on:click="buy(itemName2)">BUY</button>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input {
  margin-bottom: 8px;
}

.payment {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  width: 400px;
  background-color: #42b983;
  margin-bottom: 8px;
}

label {
  font-size: 20px;
  font-weight: bold;
}
</style>
