<script lang="ts">
export default {
  props: {
    texto: { type: String, required: true },
  }
}
</script>

<template>
    <button class="paragrafo-lg botao-principal">
      {{ texto }}
    </button>
  </template>

<style scoped>
    button{
        background: orangered;
        color: white;
        width: 250px;
        height: 60px;
        border-radius: 50px;
        font-size: 20px;
        cursor: pointer;
    }
    button:hover{
        background-color: green;
    }

</style>