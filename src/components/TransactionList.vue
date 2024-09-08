<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
      {{ transaction.text }} <span>${{ transaction.amount }}</span>
      <button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
    </li>
  </ul>
</template>
<script setup>
// props
const props = defineProps({
  transactions: {
    type: Array,
    required: true
  }
})

// emits
const emits = defineEmits(["transactionDeleted"]);

//functions
const deleteTransaction = (id) => {
  emits("transactionDeleted", id);
}
</script>