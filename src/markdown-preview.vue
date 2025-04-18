<template>
    <div id="app">
      <h1>Markdown Previewer</h1>
      <div class="container">
        <textarea
          v-model="markdownText"
          placeholder="Enter markdown here"
          class="input-area"
        ></textarea>
        <div class="preview" v-html="compiledMarkdown"></div>
      </div>
      <!-- Clear Button -->
      <button @click="clearInput" class="clear-btn">Clear</button>
    </div>
  </template>
  
  <script>
  // Import the marked library to compile markdown
  import { marked } from 'marked';
  
  export default {
    name: 'App',
    data() {
      return {
        markdownText: '# Welcome to Markdown Previewer\n\nThis is a **Markdown** editor.\n\n- Item 1\n- Item 2\n- Item 3',
      };
    },
    computed: {
      compiledMarkdown() {
        // Convert markdown text to HTML
        return marked(this.markdownText);
      },
    },
    methods: {
      // Method to clear the input text area
      clearInput() {
        this.markdownText = '';
      },
    },
  };
  </script>
  
  <style scoped>
  * {
    box-sizing: border-box;
  }
  
  body {
    font-family: Arial, sans-serif;
  }
  
  #app {
    padding: 20px;
  }
  
  .container {
    display: flex;
    gap: 20px;
  }
  
  .input-area {
    width: 50%;
    height: 300px;
    padding: 10px;
    border: 1px solid #ccc;
    font-size: 16px;
  }
  
  .preview {
    width: 50%;
    padding: 10px;
    border: 1px solid #ccc;
    background-color: #f9f9f9;
    font-size: 16px;
  }
  
  /* Styling for the clear button */
  .clear-btn {
    margin-top: 20px;
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }
  
  .clear-btn:hover {
    background-color: #0056b3;
  }
  </style>


<!-- # Markdown Previewer

Welcome to the **Markdown Previewer**. This app allows you to preview your markdown as you type.

## Features

- **Live Preview**: See the result instantly.
- **Support for Common Syntax**: Markdown supports headings, lists, links, and more.

## Syntax Examples

### Headers

# This is an H1 Header
## This is an H2 Header
### This is an H3 Header -->
