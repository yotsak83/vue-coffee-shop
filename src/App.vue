<script setup lang="ts">
import { ref } from 'vue'

let id = 0

const coffeeList = ref([
  { id: id++, name: 'Espresso', price: 3.99, count: 0 },
  { id: id++, name: 'Cappuccino', price: 4.99, count: 0 },
  { id: id++, name: 'Latte', price: 4.49, count: 0 },
  { id: id++, name: 'Mocha', price: 5.49, count: 0 }
])

function add(coffee) {
  coffee.count++
}

function remove(coffee) {
  coffee.count--
}

const count = ref(0)
</script>

<template>
  <header class="header">
    <h1>Undefined Roastery Online Order</h1>
  </header>
  <div class="order">
    <h2>Your Order</h2>
    <p>
      Total: ${{
        coffeeList.reduce((total, coffee) => total + coffee.price * coffee.count, 0).toFixed(2)
      }}
    </p>
  </div>
  <main>
    <ul class="coffee-list">
      <li v-for="coffee in coffeeList" :key="coffee.id" class="coffee-item">
        <div>{{ coffee.name }} - ${{ coffee.price }}</div>
        <div>
          <button @click="add(coffee)">Add</button>
          <button @click="remove(coffee)">Remove</button>
          <input type="text" v-model="coffee.count" />
        </div>
      </li>
    </ul>
  </main>
</template>

<style scoped>
.header {
  text-align: center;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background-color: #fff;
  padding: 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
main {
  margin: 10px;
}
.coffee-item {
  list-style: none;
  background-color: #f2f2f2;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  font-size: 16px;
  color: #333;
}
button {
  margin: 2px;
}
.order {
  text-align: center;
}
</style>
