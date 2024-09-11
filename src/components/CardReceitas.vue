<script lang="ts">
import type { PropType } from 'vue';
import type IReceita from '@/interfaces/IReceita'

    
    export default{
        props:{
            receita: {
                type: Object as PropType<IReceita>, required: true}
        }
    }
</script>

<template>
    <article class="receita">
        <img :src="`/imagens/receitas/${receita.imagem}`" alt="">
        <h3>{{ receita.nome }}</h3>
    </article>
</template>

<style scoped>
    img{
        border-radius: 30px 30px 0 0;
        width: 300px;
        height: 200px;
    }
    .receita{
        background: white;
        border-radius: 30px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    h3{
        padding-top: 10px;;
        height: 50px;
        text-align: center;
    }

</style>