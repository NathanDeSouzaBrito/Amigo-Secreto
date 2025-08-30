<template>
  <ul>
    <li v-for="p in persons" :key="p.id">
      <div v-if="editId === p.id">
        <input v-model="editForm.name" placeholder="Nome" />
        <input v-model="editForm.email" placeholder="Email" />
        <button @click="saveEdit(p.id)">Salvar</button>
        <button @click="cancelEdit">Cancelar</button>
      </div>
      <div v-else>
        {{ p.name }} - {{ p.email }}
        <button @click="startEdit(p)">Editar</button>
        <button @click="onDelete(p.id)">Remover</button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: ["persons", "onDelete", "onUpdate"],
  data() {
    return {
      editId: null,
      editForm: { name: "", email: "" },
    };
  },
  methods: {
    startEdit(person) {
      this.editId = person.id;
      this.editForm = { name: person.name, email: person.email };
    },
    cancelEdit() {
      this.editId = null;
      this.editForm = { name: "", email: "" };
    },
    saveEdit(id) {
      this.onUpdate(id, this.editForm);
      this.cancelEdit();
    },
  },
};
</script>
