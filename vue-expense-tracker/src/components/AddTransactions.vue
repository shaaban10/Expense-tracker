<template>
<h3>Add new transaction</h3>
      <form id="form" @submit.prevent="onSubmit">
        
          <label for="text">Text</label>
          <input type="text" id="text" v-model="text" placeholder="Enter text..." />
        
        
          <label for="amount"
            >Amount <br />
            (negative - expense, positive - income)</label
          >
          <input type="text" v-model="amount" id="amount" placeholder="Enter amount..." />
        
        <button class="btn">Add transaction</button>
      </form>
   

</template>
<script  setup>
import {  ref } from "vue";
import { useToast } from "vue-toastification";
import { defineEmits } from 'vue';



const text = ref('');
const amount = ref('');

const emit = defineEmits(['transactionsubmitted']);
const toast = useToast();


const onSubmit = ()=>{
  if (!text.value || !amount.value ) {
    toast.error('Both field must be filled')
  }
  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value) ,
  }
  emit('transactionsubmitted',transactionData) 
}
text.value = "";
amount.value = "";
</script>