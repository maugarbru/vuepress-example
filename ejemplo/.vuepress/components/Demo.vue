<template>
  <div>
    <h3>Hola mundo desde Vue</h3>

    <div>
      <ul>
        <li v-for="(item, index) in lista" :key="index">
          ( {{ index + 1 }} ) {{item.nombre}} {{item.apellido}} 
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      lista: [
        { nombre: "Mauricio", apellido: "Garzon" },
        { nombre: "Carlos", apellido: "Cotera" },
        { nombre: "Andres", apellido: "Granda" },
        { nombre: "Santiago", apellido: "Urrego" }
      ]
    };
  }
};
</script>