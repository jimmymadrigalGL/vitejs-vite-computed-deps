<template>
  <div>
    Counts: <br />
    &nbsp;&nbsp;- count1 = {{ count1 }} <button @click="count1++">Add 1</button
    ><br />
    &nbsp;&nbsp;- count2 = {{ count2 }} <button @click="count2++">Add 2</button
    ><br />
    &nbsp;&nbsp;- count3 = {{ count3 }} (not in calc)
    <button @click="count3++">Add 3</button><br />
    &nbsp;&nbsp;- count4 = {{ count4 }} <b>(not a ref!) </b>
    <button @click="count4++">Add 4</button>
  </div>
  <br />
  <div>Calculated: count 1 + count2 + count4 = {{ calc }}</div>
</template>

<script setup>
import { ref, computed } from 'vue';
const count1 = ref(0);
const count2 = ref(0);
const count3 = ref(0);
let count4 = 0;

const calc = computed(() => {
  console.log(
    'calculated!',
    count1.value + count2.value,
    '=',
    count1.value,
    '+',
    count2.value,
    '+',
    count4
  );
  return count1.value + count2.value + count4;
});
</script>
