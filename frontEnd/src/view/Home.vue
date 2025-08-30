<template>
  <div>
    <h1>Amigo Secreto 🎁</h1>

    <PersonForm :onAdd="addPerson" />
    <PersonList
      :persons="persons"
      :onDelete="removePerson"
      :onUpdate="updatePerson"
    />

    <button @click="draw">Sortear</button>
  </div>
</template>

<script>
import api from "../services/api";
import PersonForm from "../components/PersonForm/index.vue";
import PersonList from "../components/PersonList/index.vue";

export default {
  components: { PersonForm, PersonList },
  data() {
    return {
      persons: [],
    };
  },
  mounted() {
    this.loadPersons();
  },
  methods: {
    async loadPersons() {
      const res = await api.get("/persons");
      this.persons = res.data;
    },
    async addPerson(person) {
      await api.post("/persons", person);
      this.loadPersons();
    },
    async removePerson(id) {
      await api.delete(`/persons/${id}`);
      this.loadPersons();
    },
    async updatePerson(id, updated) {
      await api.put(`/persons/${id}`, updated);
      this.loadPersons();
    },
    async draw() {
      await api.post("/persons/draw");
      alert("Sorteio realizado! Emails enviados (veja no Ethereal).");
    },
  },
};
</script>
