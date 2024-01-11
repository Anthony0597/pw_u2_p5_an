<template>
  <p type="Id:">
    <input v-model="id" type="text" @keypress="presionandoTeclaApe" />
  </p>
  <p type="Name:"><input v-model="name" type="text" /></p>
  <p type="Weigth:"><input v-model="weight" type="text" /></p>
  <p type="Base experience:"><input v-model="experience" type="text" /></p>
</template>

<script>
export default {
  data() {
    return {
      id: null,
      name: null,
      weight: null,
      experience: null,
    };
  },
  methods: {
    async consumirAPI(id) {
      const { name, weight, base_experience } = await fetch(
        "https://pokeapi.co/api/v2/pokemon/" + id
      ).then((respuesta) => respuesta.json());
      this.name = name;
      this.weight = weight;
      this.experience = base_experience;
    },

    presionandoTeclaApe({ charCode }) {
      if (charCode === 13) {
        this.consumirAPI(this.id);
      }
    },
  },
};
</script>

<style scoped>
input {
  background-color: rgb(90, 99, 215);
  color: white;
  border-radius: 8px;
  padding: 5px;
}
label {
  text-align: left;
}
p:before {
  content: attr(type);
  display: block;
  margin: 10px 2px;
  font-size: 16px;
  color: #5a5a5a;
}
</style>