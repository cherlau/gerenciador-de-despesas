<template>
    <h3>Adicionar nova transação</h3>
    <form id="form" @submit.prevent="onSubmit">
      <div class="form-control">
        <label for="text">Título</label>
        <input type="text" id="text" v-model="text" placeholder="Título da transação..." />
      </div>
      <div class="form-control">
        <label for="amount"
          >Valor <br />
          (valor negativo - despesa, positivo - ganho)</label
        >
        <input
          type="text"
          id="amount"
          v-model="amount"
          placeholder="Insira o valor..."
        />
      </div>
      <button class="btn">Add transaction</button>
    </form>
  </template>

<script setup>
import { ref } from 'vue'
import {useToast} from 'vue-toastification'

const text = ref('')
const amount = ref('')

const emit = defineEmits(['transactionSubmitted'])

const toast = useToast()

const onSubmit = () => {
  if(!text.value || !amount.value){
    toast.error('Ambos os campos devem estar preenchidos')
    return
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value)
  }

  emit('transactionSubmitted', transactionData)

  text.value = ''
  amount.value = ''
}

</script>