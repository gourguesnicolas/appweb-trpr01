<script setup lang="ts">
import { defineProps, defineEmits } from "vue";

const props = defineProps<{
  produit: { nom: string; prix: number; quantite: number; description: string };
}>();
const emit = defineEmits(["fermer"]);
</script>

<template>
  <div class="overlay">
    <div class="popup">
      <h3>Détails du produit</h3>
      <p><strong>Nom :</strong> {{ props.produit.nom }}</p>
      <p><strong>Prix :</strong> {{ props.produit.prix }}</p>
      <p><strong>Quantité :</strong> {{ props.produit.quantite }}</p>
      <p><strong>Description :</strong> {{ props.produit.description }}</p>
      <button @click="emit('fermer')">Terminer</button>
    </div>
  </div>
</template>

<style scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.popup {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  text-align: center;
}

button {
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 5px;
  background: #2fbb16;
  color: white;
  cursor: pointer;
  transition: 0.5s;
}

button:hover {
  background: rgb(41, 155, 21);
  transition: 0.5s;
}
</style>
