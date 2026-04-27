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
  #app { 
    font-family: sans-serif; 
    padding: 20px; 
    max-width: 500px; 
    margin: 0 auto;
  }

  h1, h2, h3 {
    color: #333;
  }

  .input-section {
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 5px;
    flex-wrap: wrap;
  }

  .input-section h3 {
    width: 100%;
    margin-bottom: 10px;
  }

  button { 
    cursor: pointer; 
    padding: 8px 12px;
    border-radius: 4px;
    border: 1px solid #ccc;
    background-color: #f0f0f0;
    transition: background-color 0.2s;
  }
  
  button:hover {
    background-color: #e0e0e0;
  }

  .btn-remove { 
    padding: 4px 8px; 
    font-size: 0.9em; 
    background-color: #ffdddd;
    border-color: #ffcccc;
  }
  
  .btn-remove:hover {
    background-color: #ffcccc;
  }

  input { 
    flex-grow: 1;
    padding: 8px; 
    border-radius: 4px; 
    border: 1px solid #ccc; 
  }

  hr {
    border: 0;
    height: 1px;
    background-color: #ddd;
    margin: 20px 0;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    background: #f9f9f9;
    margin: 8px 0;
    padding: 10px 15px;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 1px solid #eee;
  }

  .empty-message {
    color: #888;
    text-align: center;
    padding: 30px;
    background-color: #fdfdfd;
    border: 1px dashed #ccc;
    border-radius: 8px;
  }
</style>
