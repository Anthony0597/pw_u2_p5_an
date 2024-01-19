<template>
  <div class="container">
    <img :src="urlImg" alt="No se puede cargar" />
    <label for="">{{ texto }}</label>
  </div>
</template>

<script>
export default {
  props: {
    texto: {
      type: String,
    },
    urlImg: {
      type: String,
    },
  },
};
</script>

<style scoped>
img {
  width: 200px;
  height: 300px;
}
.container {
  display: block;
}
</style>