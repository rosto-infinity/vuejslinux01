<script setup>
import {ref} from 'vue'
const details = ref(
      [
      '50% aaaa',
      '50% bbb',
      '80% cccc',
      '90% ddd',
    ]
)
const variants = ref(
      [
      {id:784, color: 'green'},
      {id:785, color: 'blue'},
    ]
)
</script>

<template>
      <ul>
        <li  v-for="detail in details"> {{ detail }} </li>
       </ul>
       <hr>
      <ul>
        <ul> 
            <li  v-for="variant in variants" :key="variant.id">
                  {{ variant.id}} |{{ variant.color}}
             </li>
        </ul>
       </ul>


</template>
