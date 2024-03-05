<template>
  <div>
    <button @click="createPromise1">createPromise1</button>
    <button @click="createPromise2">createPromise2</button>
    <button @click="createPromise3">createPromise3</button>
    <button @click="subscriber1">消费1</button>
    <button @click="subscriber2">消费2</button>
    <button @click="subscriber3">消费3</button>
  </div>
</template>

<script setup>

const types = {
  promiseFlag1: 'promiseFlag1',
  promiseFlag2: 'promiseFlag2',
  promiseFlag3: 'promiseFlag3',
}
const resolveMap = new Map();
resolveMap.set(types.promiseFlag1, []);
resolveMap.set(types.promiseFlag2, []);
resolveMap.set(types.promiseFlag3, []);

function createPromise1() {
  createPromise(types.promiseFlag1).then(n => {
    console.log(types.promiseFlag1, n)
  })
}
function createPromise2() {
  createPromise(types.promiseFlag2).then(n => {
    console.log(types.promiseFlag2, n)
  })
}
function createPromise3() {
  createPromise(types.promiseFlag3).then(n => {
    console.log(types.promiseFlag3, n)
  })
}

function subscriber1() {
  let n = Math.floor(Math.random() * 10);
  const fns = resolveMap.get(types.promiseFlag1);
  fns.length && fns.shift()(n);
  console.log("map", resolveMap)
}
function subscriber2() {
  let n = Math.floor(Math.random() * 10);
  const fns = resolveMap.get(types.promiseFlag2);
  fns.length && fns.shift()(n);
  console.log("map", resolveMap)
}
function subscriber3() {
  let n = Math.floor(Math.random() * 10);
  const fns = resolveMap.get(types.promiseFlag3);
  fns.length && fns.shift()(n);
  console.log("map", resolveMap)
}

function createPromise(type) {
  return new Promise((resolve) => {
    resolveMap.get(type).push(resolve);
  })
}
</script>

<style scoped>
</style>
