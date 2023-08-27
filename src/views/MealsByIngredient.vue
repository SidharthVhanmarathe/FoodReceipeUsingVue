<template>
<div class="p-8 pb-0">
   <h1 class="text-4xl font-bold mb-4
    text-orange-500">Meals for {{ ingredient.strIngredient }}</h1>

</div>

   <Meals :meals="meals" />
</template>
<script setup>
import {  onMounted ,watch} from 'vue';
import store from '../store';
import {computed} from '@vue/reactivity';
import { useRoute } from 'vue-router';
import Meals from '../views/Meals.vue';
const route=useRoute();
const ingredient=computed(()=>store.state.ingredient)
const meals=computed(()=> store.state.mealsByIngredient)

watch(route,()=>
{
    store.dispatch('searchMealsByIngredient',route.params.ingredient)

})
onMounted(()=>
{
   store.dispatch('searchMealsByIngredient',route.params.ingredient)
})
</script>
