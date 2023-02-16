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
    <button @click="count4++">Add 4</button><br />
    &nbsp;&nbsp;- mult = {{ mult }}
    <input type="checkbox" value="{mult}" @click="mult = !mult" /><br />
    &nbsp;&nbsp;- by = {{ by }} <button @click="by++">Add By</button><br />
  </div>
  <br />
  <div>Calculated: mult-by * (count 1 + count2 + count4 ) = {{ calc }}</div>
  <button @click="reset">Reest</button>
</template>

<script setup>
import { ref, computed } from 'vue';
import { useMemoize } from '@vueuse/core';

const count1 = ref(0);
const count2 = ref(0);
const count3 = ref(0);
let count4 = 0;
const mult = ref(false);
const by = ref(1);

const memoCalc = useMemoize((a, b, c, e) => {
  const result = e * (a + b + c);
  console.log('calculated!', result, '=', e, '* (', a, '+', b, '+', c, ')');
  return result;
});

const calc = computed(() =>
  memoCalc(count1.value, count2.value, count4, mult.value ? by.value : 1)
);

const reset = () => {
  count1.value = 0;
  count2.value = 0;
  count3.value = 0;
  count4 = 0;
};
</script>
