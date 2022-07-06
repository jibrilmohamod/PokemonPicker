<template>
 <div class="w-full flex justify-center">
  <input
   type="text"
   placeholder="Enter Pokemon Here"
   class="mt-10 p-2 border-blue-500 border-2"
   v-model="text"
  />
 </div>
 <div class="mt-10 p-4 flex flex-wrap justify-center">
  <div
   class="ml-4 text-2xl text-blue-600"
   v-for="(pokemon, idx) in filteredPokemon"
   :key="idx"
  >
   <router-link :to="`/about/${urlIdLookup[pokemon.name]}`">
    {{ pokemon.name }} </router-link
   >s
  </div>
 </div>
</template>

<script>
 import { reactive, toRefs, computed } from "vue"

 export default {
  setup() {
   const state = reactive({
    pokemons: [],
    urlIdLookup: {},
    text: "",
    filteredPokemon: computed(() => updatePokemon()),
   })

   fetch("https://pokeapi.co/api/v2/pokemon?limit=100")
    .then((response) => response.json())
    .then((data) => {
     state.pokemons = data.results
     state.urlIdLookup = data.results.reduce(
      (acc, curr, idx) => ({ ...acc, [curr.name]: idx + 1 }),
      {}
     )
    })
    .catch((error) => console.error(error))
    .finally(() => console.log("fetch complete"))

   function updatePokemon() {
    if (!state.text) {
     return []
    }
    return state.pokemons.filter((pokemon) => pokemon.name.includes(state.text))
   }
   return { ...toRefs(state) }
  },
 }
</script>

<style lang="scss" scoped></style>
