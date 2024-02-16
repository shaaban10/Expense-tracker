<template>
  <Header />
  <div class="container">
  <Balance :total="+total" />
  </div>
  <div class="inc-exp-container">
    <IncomeExpensence :income="+income" :expenses="+expenses"/>
  </div>
  <TransactionsList :transactions="transactions" @itemdeleted="handletransactiondeletted" />
  <div class="form-control">
<AddTransactions @transactionsubmitted="handletransactionsubmitted" />
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
import { useToast } from "vue-toastification";
 
const toast = useToast();
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

// Add Transaction
const handletransactionsubmitted = (transactionData)=>{
transactions.value.push({
  id: generateUniqueId(),
  text: transactionData.text,
  amount: transactionData.amount,
});
toast.success('Transaction added'); 
}
const generateUniqueId=()=>{
  return Math.floor(Math.random()*1000000);
}
const handletransactiondeletted= (id)=>{
transactions.value  = transactions.value.filter((transactions)=>
transactions.id !==id);
toast.success('transaction deleted')
}
</script>
