<template>
  <div>
    <section>
      <div class="block" v-for="pos in menu" :key="pos.name">
        <div class="info">
          <h3>{{ pos.name }}</h3>
          <p>{{ pos.price }}</p>
        </div>
        <div class="buy">
          <button v-if="!pos.isBought" @click="buy(pos)">Купить</button>
          <div v-else>
            <button @click="decrease(pos)">-</button>
            <input type="number" min="0" :value="pos.quantity" disabled />
            <button @click="increase(pos)">+</button>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface MenuItem {
  name: string;
  price: number;
  isBought: boolean;
  quantity: number;
}

const menu = ref<MenuItem[]>([
  { name: 'Бургер', price: 500, isBought: false, quantity: 0 },
  { name: 'Донер', price: 500, isBought: false, quantity: 0 },
  { name: 'Пицца', price: 500, isBought: false, quantity: 0 },
  { name: 'Рамен', price: 500, isBought: false, quantity: 0 },
  { name: 'Суши', price: 500, isBought: false, quantity: 0 }
])

const buy = (item: MenuItem) => {
  item.isBought = true
  item.quantity = 1
}

const increase = (item: MenuItem) => {
  item.quantity++
}

const decrease = (item: MenuItem) => {
  if (item.quantity > 1) {
    item.quantity--
  }
  else{
    item.isBought = false
  }
}
</script>

<style scoped>
section {
  display: flex;
}
.block {
  border: 1px solid black;
}
</style>
