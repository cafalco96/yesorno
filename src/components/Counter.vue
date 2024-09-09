<script setup>
import {ref, computed, defineProps} from 'vue'
const props = defineProps({
  text: String,
  start: {
    type: Number,
    // required: true
    default:1,
    validator(value){
      return value<100 && value > 0
    }
  }
})
const getSquareValue = computed(()=>number.value*number.value) 
const customTitle = computed(()=> props.text ? props.text : 'Counter')
const number = ref(props.start)
const increase = ()=>number.value++
const decrease = ()=>number.value--
</script>
<template>
  <h2>{{ customTitle }}</h2>
  <p>{{ number }} <sup>2</sup> = {{ getSquareValue }}</p>
  <div>
    <button @click="increase">+1</button>
    <button @click="decrease">-1</button>
  </div>
</template>
<style scoped>
button {
  background-color: #64bb87;
  border-radius: 5px;
  color: white;
  margin: 0 5px;
  padding: 5px 15px;
  transition: 0.3s ease-in-out;
}
</style>