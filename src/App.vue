<script setup>
 import { RouterLink, RouterView } from "vue-router"
</script>

<template>
 <div>
  <header>
   <nav class="p-14">
    <RouterLink class="flex justify-center text-4xl text-yellow-700" to="/"
     >Pockemon Picker</RouterLink
    >
   </nav>
  </header>
 </div>

 <RouterView />
</template>
