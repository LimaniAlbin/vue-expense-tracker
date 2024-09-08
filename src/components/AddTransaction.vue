<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount"
      >Amount <br/>
        (negative - expense, positive - income)</label
      >
      <input type="number" id="amount" placeholder="Enter amount..." v-model="amount" />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>

//data
import {ref} from "vue";
import {useToast} from "vue-toastification";

// initialization
const toast = useToast();

//emits
const emits = defineEmits(["transactionSubmitted"]);

const text = ref('')
const amount = ref('')

// functions
const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error('Both fields must be filled')
    return
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  }

  emits("transactionSubmitted", transactionData);

  text.value = ''
  amount.value = ''
}
</script>