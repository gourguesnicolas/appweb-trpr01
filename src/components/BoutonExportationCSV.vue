<script setup lang="ts">
import { defineProps } from "vue";

const props = defineProps<{
  produits: {
    nom: string;
    prix: number;
    quantite: number;
    description: string;
  }[];
}>();

// SOURCE: ChatGPT
const exporterCSV = () => {
  const enTetes = "Nom,Prix,Quantité,Description\n";
  const lignes = props.produits
    .map(
      (produit) =>
        `${produit.nom},${produit.prix},${produit.quantite},${produit.description}`
    )
    .join("\n");
  const contenu = enTetes + lignes;

  const blob = new Blob([contenu], { type: "text/csv" });
  const url = URL.createObjectURL(blob);

  const lien = document.createElement("a");
  lien.href = url;
  lien.download = "produits.csv";
  document.body.appendChild(lien);
  lien.click();
  document.body.removeChild(lien);

  URL.revokeObjectURL(url);
};
</script>

<template>
  <div>
    <button @click="exporterCSV">
      <!-- SOURCE: https://icons.getbootstrap.com/icons/file-earmark-arrow-down/ -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-file-earmark-arrow-down"
        viewBox="0 0 16 16"
      >
        <path
          d="M8.5 6.5a.5.5 0 0 0-1 0v3.793L6.354 9.146a.5.5 0 1 0-.708.708l2 2a.5.5 0 0 0 .708 0l2-2a.5.5 0 0 0-.708-.708L8.5 10.293z"
        />
        <path
          d="M14 14V4.5L9.5 0H4a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h8a2 2 0 0 0 2-2M9.5 3A1.5 1.5 0 0 0 11 4.5h2V14a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1h5.5z"
        />
      </svg>
    </button>
  </div>
</template>

<style scoped>
button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 0.25rem;
  cursor: pointer;
  transition: 0.5s;
}

button:hover {
  background-color: #0056b3;
  transition: 0.5s;
}
</style>
