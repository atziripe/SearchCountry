<template>
<div class="row">
    <div class="col-12" v-for="pais in paises" :key="pais.name">
        <Card :pais="pais"/>
    </div>
</div>
</template>

<script>
import { computed, onMounted } from 'vue'
import {useStore} from 'vuex'
import Card from './Card.vue'
export default {
    components:{
        Card
    },
    setup(){
        const store = useStore()

        const paises = computed(() => {
            return store.getters.topPaisesPoblacion //getter que ordena los paises segun su poblacion
            //return store.state.paises //Tomar un stado del store mediante una propiedad computada
        })

        onMounted(async() => {
            await store.dispatch('getPaises') //Ejecutar un action del store
            await store.dispatch('filtrarRegion','Americas')
        })

        return {paises}
    }
}
</script>

<style>

</style>