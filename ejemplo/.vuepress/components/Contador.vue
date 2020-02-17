<template>
  <div>
    <h3>Hola mundo desde Vue</h3>

    <div>
      <h4>Contador: {{contador}}</h4>
      <button @click="contador -= -1">+</button>
      <button @click="contador--">-</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      contador: 0
    };
  }
};
</script>