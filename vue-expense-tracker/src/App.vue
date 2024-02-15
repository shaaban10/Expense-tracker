<template>
  <Header />
  <div class="container">
  <Balance />
  </div>
  <div class="inc-exp-container">
    <IncomeExpensence />
  </div>
  <TransactionsList />
  <div class="form-control">
<AddTransactions />
    <div class="form-control">

    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpensence from './components/IncomeExpensence.vue'
import TransactionsList from './components/TransactionsList.vue'
import AddTransactions from './components/AddTransactions.vue'
export default {
  components: {
    Header,
    Balance,
    IncomeExpensence,
    TransactionsList,
    AddTransactions


  },
};
</script>
