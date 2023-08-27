<template>
    <div class="p-8 pb-8">
        <h1 class="text-4xl font-bold mb-4 text-orange-500">Meals By Letter</h1>
    </div>
    <div class="flex justify-center gap-2 mt-2">
        <router-link :to="{name: 'byLetter',params:{ letter }}"
        v-for="letter of letters"
        :keys="letter" 
        class="hover:text-orange-500 transition-colors">
        {{ letter }}
    </router-link>
</div>   
  
 <Meals :meals="meals"/>

</template>

<script setup>
import store from '../store';
import Meals from '../views/Meals.vue';
import {onMounted ,watch} from 'vue';
import {computed} from '@vue/reactivity';
import {useRoute} from 'vue-router';
const route = useRoute();

const letters="ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals=computed(()=> store.state.mealsByLetter);

watch(route,()=>
{
    store.dispatch("searchMealsByLetter",route.params.letter);

});
onMounted(()=>
{
    store.dispatch("searchMealsByLetter",route.params.letter);
});

</script>