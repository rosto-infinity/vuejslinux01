<script setup>
import {ref} from 'vue'

const count = ref(0)

const increment = () =>{
  count.value +=1
}
const decrement = () =>{
  count.value -=1
}

</script>

<template>
   <h1 class="text-center"> Compteur {{ count }}</h1>
  <button  @click="increment" class="button">Increment</button>
  <button  @click="decrement"  class="button">Decrement</button>
  <div v-if="count >=5" class="text-green-700 pl-12" >OK++++>>>>>>>>>>>>>></div>
  <div v-else-if="(count >0 && count <5)" class="text-red-700 pl-12" >OK----<<<<<<<<<<<<<<<<< </div>
  <div v-else  class="text-orange-400 pl-12" >OK00000000000000000000</div>
</template>

<style scoped>
</style>
