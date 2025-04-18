<template>
    <div class="app">
      <div class="quote-card">
        <p class="quote">“{{ currentQuote.text }}”</p>
        <p class="author">— {{ currentQuote.author }}</p>
        <button @click="getRandomQuote">New Quote</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  
  const quotes = [
    { text: "Life is what happens when you're busy making other plans.", author: "John Lennon" },
    { text: "Be yourself; everyone else is already taken.", author: "Oscar Wilde" },
    { text: "The only way to do great work is to love what you do.", author: "Steve Jobs" },
    { text: "If you tell the truth, you don't have to remember anything.", author: "Mark Twain" },
    { text: "Simplicity is the ultimate sophistication.", author: "Leonardo da Vinci" },
  ]
  
  const currentQuote = ref({ text: '', author: '' })
  
  const getRandomQuote = () => {
    const index = Math.floor(Math.random() * quotes.length)
    currentQuote.value = quotes[index]
  }
  
  onMounted(getRandomQuote)
  </script>
  
  <style scoped>
  body, html {
    margin: 0;
    padding: 0;
    font-family: 'Segoe UI', sans-serif;
  }
  
  .app {
    background: #1e293b;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
  }
  
  .quote-card {
    background: #0f172a;
    color: #f8fafc;
    max-width: 500px;
    width: 100%;
    border-radius: 16px;
    padding: 30px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
    text-align: center;
  }
  
  .quote {
    font-size: 1.5rem;
    margin-bottom: 20px;
  }
  
  .author {
    font-size: 1rem;
    color: #94a3b8;
    margin-bottom: 30px;
  }
  
  button {
    background: #f8fafc;
    color: #0f172a;
    border: none;
    padding: 12px 24px;
    font-size: 1rem;
    border-radius: 8px;
    cursor: pointer;
    transition: background 0.2s ease;
  }
  
  button:hover {
    background: #e2e8f0;
  }
  </style>
  