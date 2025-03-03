<script setup lang="ts">
import { defineProps, defineEmits } from "vue";

const props = defineProps<{ produitNom: string }>();
const emit = defineEmits(["confirmer", "annuler"]);
</script>

<template>
  <!-- SOURCE/AIDE: ChatGPT -->
  <div class="overlay">
    <div class="popup">
      <h3>Supprimer "{{ props.produitNom }}" ?</h3>
      <p>Êtes-vous sûr de vouloir supprimer ce produit ?</p>
      <div class="actions">
        <button @click="emit('annuler')" class="annuler">Annuler</button>
        <button @click="emit('confirmer')" class="confirmer">Confirmer</button>
      </div>
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

.actions {
  margin-top: 1rem;
  display: flex;
  justify-content: space-around;
}

button {
  padding: 0.5rem 1rem;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.annuler {
  background: #aaa;
  color: white;
}

.confirmer {
  background: #af2837;
  color: white;
}

.confirmer:hover {
  background: rgb(130, 20, 32);
  transition: 0.5s;
}

.annuler:hover {
  background: #888;
  transition: 0.5s;
}
</style>
