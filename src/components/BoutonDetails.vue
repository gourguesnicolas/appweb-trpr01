<script setup lang="ts">
import { defineEmits } from "vue";

const emit = defineEmits(["details-click"]);
</script>

<template>
  <div>
    <button @click="emit('details-click')">
      <!-- SOURCE: https://icons.getbootstrap.com/icons/list/ -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-list"
        viewBox="0 0 16 16"
      >
        <path
          fill-rule="evenodd"
          d="M2.5 12a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5m0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5m0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5"
        />
      </svg>
    </button>
  </div>
</template>

<style scoped>
button {
  background-color: #2fbb16;
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
  background-color: rgb(41, 155, 21);
  transition: 0.2s;
}

svg {
  fill: white;
}
</style>
