<script setup lang="ts"></script>

<template>
  <div>
    <button>
      <!-- SOURCE: https://icons.getbootstrap.com/icons/x-circle-fill/ -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-x-circle-fill"
        viewBox="0 0 16 16"
      >
        <path
          d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0M5.354 4.646a.5.5 0 1 0-.708.708L7.293 8l-2.647 2.646a.5.5 0 0 0 .708.708L8 8.707l2.646 2.647a.5.5 0 0 0 .708-.708L8.707 8l2.647-2.646a.5.5 0 0 0-.708-.708L8 7.293z"
        />
      </svg>
    </button>
  </div>
</template>

<style scoped>
button {
  background-color: #af2837;
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
  background-color: rgb(130, 20, 32);
  transition: 0.2s;
}

svg {
  fill: white;
}
</style>
