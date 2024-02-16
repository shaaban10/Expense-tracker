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
import { ref ,computed ,onMounted} from 'vue';
import { useToast } from "vue-toastification";
 
const toast = useToast();
const transactions = ref([]);


onMounted(()=>{
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
  if (savedTransactions) {
    transactions.value = savedTransactions;
  }

})
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
saveTransactionsToLocalStorage()
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
//save to localStorage
const saveTransactionsToLocalStorage = ()=>{
  localStorage.setItem('transactions',JSON.stringify(transactions.value))
}

</script>
