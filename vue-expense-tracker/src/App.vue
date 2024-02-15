<template>
  <Header />
  <div class="container">
  <Balance :total="total" />
  </div>
  <div class="inc-exp-container">
    <IncomeExpensence :income="income" :expenses="expenses"/>
  </div>
  <TransactionsList :transactions="transactions" />
  <div class="form-control">
<AddTransactions />
    <div class="form-control">

    </div>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpensence from './components/IncomeExpensence.vue'
import TransactionsList from './components/TransactionsList.vue'
import AddTransactions from './components/AddTransactions.vue'
import { ref ,computed } from 'vue';
 
const transactions = ref([
  { id: 1 ,text: 'Flower', amount: -19.99},
  { id: 2 ,text: 'Salary', amount: 199.99},
  { id: 3 ,text: 'Book', amount: -10},
  { id: 4 ,text: 'Camera', amount: 155},

  ]);
  // Get Total
const total= computed(()=>{
  return transactions.value.reduce((acc,transactions)=>{
    return acc + transactions.amount;
  },0);
});
//Get Income
const income= computed(()=>{
  return transactions.value.filter((transactions)=>transactions.amount>0)
  .reduce((acc,transactions)=>{
    return acc + transactions.amount;
  },0).toFixed(2);
}); 
const expenses = computed(()=>{
  return transactions.value.filter((transactions)=>transactions.amount<0).reduce((acc,transactions)=>{
    return acc + transactions.amount
  },0).toFixed(2)
})
</script>
