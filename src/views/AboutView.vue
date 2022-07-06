<template>
 <div>
  <div
   v-if="pokemon"
   class="w-6/12 m-auto bg-purple-200 mt-4 shadow-2xl flex justify-center flex-col items-center"
  >
   <h3 class="text-2xl text-green-900 uppercase">
    {{ pokemon.name }}
   </h3>
   <div class="flex justify-center">
    <img :src="pokemon.sprites.front_shiny" alt="" class="w-72" />
    <img :src="pokemon.sprites.back_shiny" alt="" class="w-72" />
   </div>
   <h4 class="text-yellow-700">types</h4>
   <div v-for="(type, index) in pokemon.types" :key="index">
    <h5 class="text-blue-700">{{ type.type.name }}</h5>
   </div>
  </div>
 </div>
</template>

<script>
 import { useRoute } from "vue-router"
 import { reactive, toRefs } from "vue"

 export default {
  setup() {
   const route = useRoute()

   const state = reactive({
    pokemon: null,
   })

   fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`).then(
    (res) =>
     res.json().then((data) => {
      console.log(data)
      state.pokemon = data
     })
   )
   return { ...toRefs(state) }
  },
 }
</script>

<style lang="scss" scoped></style>
