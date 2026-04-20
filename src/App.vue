<script setup>
import { ref } from 'vue'

const lista = ref(['Lavar a casa', 'Estudar'])
const input = ref('')
const caixaEditando = ref(null)

const add = () => {
  if (input.value.trim()) {
    lista.value.push(input.value)
    input.value = ''
  }
}
const remover = (index) => {
  lista.value.splice(index, 1)
}
const editar = (index) => {
  caixaEditando.value = index
}
const salvar = () => {
  caixaEditando.value = null
}
</script>

<template>
  <div class="min-h-screen bg-gray-100 p-8 flex flex-col items-center">
    <div class="bg-white p-6 rounded-xl shadow-lg w-full max-w-md">
      <h3 class="text-2xl font-bold text-gray-800 mb-4 border-b pb-2">Lista de Tarefas</h3>
      
      <div class="flex gap-2 mb-6">
        <input 
          type="text" 
          v-model="input" 
          placeholder="Nova tarefa..."
          class="flex-1 px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500"
          @keyup.enter="add"
        >
        <button 
          @click="add" 
          class="bg-green-500 hover:bg-green-600 text-white px-4 py-2 rounded-lg font-medium transition"
        >
          Enviar
        </button>
      </div>

      <ul class="space-y-3">
        <li 
          v-for="(fruta, index) in lista" 
          :key="index"
          class="flex items-center justify-between p-3 bg-gray-50 rounded-lg hover:bg-gray-100 transition"
        >
          <div v-if="caixaEditando === index" class="flex gap-2 w-full">
            <input 
              type="text" 
              v-model="lista[index]" 
              class="flex-1 px-2 py-1 border rounded focus:outline-none"
              @keyup.enter="salvar"
            >
            <button @click="salvar" class="text-blue-600 font-bold">OK</button>
          </div>

          <div v-else class="flex items-center justify-between w-full">
            <span class="text-gray-700 font-medium">{{ fruta }}</span>
            <div class="flex gap-2">
              <button 
                @click="editar(index)" 
                class="text-sm bg-blue-100 text-blue-600 px-3 py-1 rounded hover:bg-blue-200 transition"
              >
                Editar
              </button>
              <button 
                @click="remover(index)" 
                class="text-sm bg-red-100 text-red-600 px-3 py-1 rounded hover:bg-red-200 transition"
              >
                Remover
              </button>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>