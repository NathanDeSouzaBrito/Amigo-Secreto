<template>
  <form @submit.prevent="handleSubmit">
    <input v-model="form.name" placeholder="Nome" required />
    <input v-model="form.email" placeholder="Email" required />
    <button type="submit">Adicionar</button>
  </form>
</template>

<script>
export default {
  props: ["onAdd"],
  data() {
    return {
      form: { name: "", email: "" },
    };
  },
  methods: {
    handleSubmit() {
      this.onAdd(this.form);
      this.form = { name: "", email: "" };
    },
  },
};
</script>
