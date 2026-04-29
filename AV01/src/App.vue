<script setup lang="ts">
import { ref } from 'vue'

const novoProduto = ref('')
const cestaCompras = ref<string[]>([])

function adicionarProduto() {
  if (novoProduto.value.trim() !== '') {
    cestaCompras.value.push(novoProduto.value)
    novoProduto.value = ''
  }
}

function removerProduto(index: number) {
  cestaCompras.value.splice(index, 1)
}
</script>

<template>
  <div id="app">
    <h1>Sistema de Gestão de Compras</h1>

    <div class="input-section">
      <h3>Adicionar novo produto:</h3>
      <input 
        v-model="novoProduto" 
        @keyup.enter="adicionarProduto" 
        placeholder="Digite o nome do produto"
      >
      <button @click="adicionarProduto">Adicionar</button>
    </div>

    <hr>

    <div v-if="cestaCompras.length > 0">
      <h2>Minha Cesta de Compras</h2>
      <p><strong>Total de itens:</strong> {{ cestaCompras.length }}</p>
      
      <ul>
        <li v-for="(produto, index) in cestaCompras" :key="index">
          <span>{{ index + 1 }}. {{ produto }}</span>
          <button class="btn-remove" @click="removerProduto(index)">🗑️</button>
        </li>
      </ul>
    </div>
    
    <div v-else>
      <p class="empty-message">Sua cesta está vazia! Adicione produtos para começar.</p>
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&display=swap');

#app {
  font-family: 'Inter', sans-serif;
  max-width: 480px;
  margin: 60px auto;
  padding: 0 20px;
  color: #1e293b;
}

h1 {
  font-size: 1.6rem;
  font-weight: 600;
  margin-bottom: 24px;
  color: #1e293b;
}

h2 {
  font-size: 1.1rem;
  font-weight: 600;
  color: #334155;
  margin-bottom: 12px;
}

h3 {
  font-size: 0.8rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.8px;
  color: #94a3b8;
  margin-bottom: 8px;
  width: 100%;
}

.input-section {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

input {
  flex: 1;
  padding: 10px 14px;
  border: 1px solid #cbd5e1;
  border-radius: 8px;
  font-family: 'Inter', sans-serif;
  font-size: 0.95rem;
  color: #1e293b;
  outline: none;
  transition: border-color 0.2s;
}

input:focus {
  border-color: #6366f1;
}

input::placeholder {
  color: #94a3b8;
}

button {
  padding: 10px 18px;
  border: none;
  border-radius: 8px;
  background: #6366f1;
  color: #fff;
  font-family: 'Inter', sans-serif;
  font-size: 0.9rem;
  font-weight: 500;
  cursor: pointer;
  transition: background 0.2s;
}

button:hover {
  background: #4f46e5;
}

hr {
  border: none;
  border-top: 1px solid #e2e8f0;
  margin: 24px 0;
}

p {
  font-size: 0.9rem;
  color: #64748b;
  margin: 0 0 12px;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 14px;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  font-size: 0.95rem;
  color: #334155;
}

.btn-remove {
  padding: 4px 10px;
  font-size: 0.85rem;
  background: #fff0f0;
  color: #ef4444;
  border: 1px solid #fecaca;
  border-radius: 6px;
  cursor: pointer;
  transition: background 0.2s;
}

.btn-remove:hover {
  background: #fecaca;
}

.empty-message {
  text-align: center;
  color: #94a3b8;
  padding: 32px;
  border: 1px dashed #cbd5e1;
  border-radius: 8px;
  font-size: 0.9rem;
}
</style>
