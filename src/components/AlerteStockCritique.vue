<script setup lang="ts">
defineProps<{
  produitNom: string;
}>();

const emit = defineEmits(["fermer"]);
</script>

<template>
  <div class="overlay">
    <div class="popup">
      <h2>⚠️Quantité Critique</h2>
      <p>
        Le stock du produit <strong>{{ produitNom }}</strong> est en dessous du
        seuil critique!
      </p>
      <button @click="emit('fermer')">OK</button>
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
  justify-content: center;
  align-items: center;
}

.popup {
  background: white;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

button {
  margin-top: 10px;
  padding: 8px 15px;
  border: none;
  border-radius: 5px;
  background-color: red;
  color: white;
  cursor: pointer;
  font-weight: bold;
  transition: 0.5s;
}

button:hover {
  background-color: darkred;
  transition: 0.5s;
}
</style>
