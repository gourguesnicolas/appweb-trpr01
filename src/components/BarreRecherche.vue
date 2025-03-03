<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits(["recherche"]);
const recherche = ref("");

const mettreAJourRecherche = () => {
  emit("recherche", recherche.value);
};
</script>

<template>
  <div class="barreRecherche">
    <h2>Rechercher un produit</h2>
    <div class="inputBoutonGroup">
      <input
        type="search"
        placeholder="Rechercher un produit"
        v-model="recherche"
        @input="mettreAJourRecherche"
      />
    </div>
  </div>
</template>

<style scoped>
.barreRecherche {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 10px;
  padding: 1rem;
  margin-bottom: 10px;
  background-color: #e5e6e0;
  border-radius: 5px;
  box-shadow: 0 0 1rem #00000033;
}

.inputBoutonGroup {
  display: flex;
  gap: 1rem;
}

.barreRecherche input {
  padding: 0.5rem;
  width: 15%;
  border: 1px solid #00000033;
  border-radius: 5px;
}

.barreRecherche button {
  padding: 0.5rem;
  width: 6%;
  background-color: #18507d;
  color: white;
  border: none;
  border-radius: 5px;
  transition: 0.5s;
  cursor: pointer;
}

.barreRecherche button:hover {
  background-color: #2880c7;
  transition: 0.5s;
}
</style>
