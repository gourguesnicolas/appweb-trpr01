<script setup lang="ts">
import { defineEmits } from "vue";

const emit = defineEmits(["dupliquer"]);
</script>

<template>
  <div>
    <button @click="emit('dupliquer')">
      <!-- SOURCE: https://icons.getbootstrap.com/icons/front/ -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-front"
        viewBox="0 0 16 16"
      >
        <path
          d="M0 2a2 2 0 0 1 2-2h8a2 2 0 0 1 2 2v2h2a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2v-2H2a2 2 0 0 1-2-2zm5 10v2a1 1 0 0 0 1 1h8a1 1 0 0 0 1-1V6a1 1 0 0 0-1-1h-2v5a2 2 0 0 1-2 2z"
        />
      </svg>
    </button>
  </div>
</template>

<style scoped>
button {
  background-color: rgb(28, 101, 153);
  border: none;
  border-radius: 5px;
  width: 25px;
  height: 25px;
  padding: 1px;
  box-shadow: 0 0 1rem #00000033;
  cursor: pointer;
  transition: 0.2s;
}

button:hover {
  background-color: rgb(13, 68, 107);
  transition: 0.2s;
}

svg {
  fill: white;
}
</style>
