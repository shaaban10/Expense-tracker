<template>
<h3>Add new transaction</h3>
      <form id="form">
        
          <label for="text">Text</label>
          <input type="text" id="text" placeholder="Enter text..." />
        
        
          <label for="amount"
            >Amount <br />
            (negative - expense, positive - income)</label
          >
          <input type="number" id="amount" placeholder="Enter amount..." />
        
        <button class="btn">Add transaction</button>
      </form>
   

</template>