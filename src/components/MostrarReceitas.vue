<script lang="ts">
import type IReceita from '@/interfaces/IReceita';
import { obterReceitas } from '@/http/index';
import CardReceitas from './CardReceitas.vue';
import BotaoPrincipal from './BotaoPrincipal.vue';
import type { PropType } from 'vue';
import { itensDeLista1EstaoEmLista2 } from '@/operacoes/listas';

export default{
    props:{
        ingredientes: { type: Array as PropType<string[]>, required: true}
    },
    components:{CardReceitas, BotaoPrincipal},
    data(){
        return{
            receitasEncontradas:[] as IReceita[]
        }
    },
    async created(){
        const receitas = await obterReceitas();

        this.receitasEncontradas = receitas.filter((receita) =>{
            //Lógica que verifica se posso fazer receita:
            //Todos os ingredientes de uma receita devem estar inclusos na minha lista de ingredientes

            const possoFazerReceita = itensDeLista1EstaoEmLista2(receita.ingredientes, this.ingredientes);

            return possoFazerReceita;
        })
    },
    emits:['editarLista']
    
}

</script>

<template>
    <h2>Receitas</h2>
    <span>Resultados encontrados: {{ receitasEncontradas.length }}</span>
    <p>Veja as opções de receitas que encontramos com os ingredientes que você tem por aí!</p>

    <ul class="receitas">
        <li v-for="receita in receitasEncontradas" :key="receita.nome">
            <CardReceitas
            :receita="receita"/>
        </li>
    </ul>

    <BotaoPrincipal texto="Editar lista" @click="$emit('editarLista')"/>
</template>

<style scoped>
    ul{
        display: flex;
        flex-direction: row;
        gap: 15px;
        flex-wrap: wrap;
    }

</style>