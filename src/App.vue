<script setup lang="ts">
import { ref } from "vue";
import Entete from "./components/Entete.vue";
import ListeProduits from "./components/ListeProduits.vue";

const produits = ref([
  {
    nom: "Piles AA Duracell",
    description: "Piles alcalines",
    prix: 20.69,
    quantite: 15,
  },
  {
    nom: "Clous 2 pouces",
    description: "Paquet de 64",
    prix: 5.99,
    quantite: 60,
  },
  {
    nom: "Peinture blanche 1L",
    description: "La meilleure de la ville et des environs",
    prix: 15.99,
    quantite: 10,
  },
]);

const ajouterProduit = (produit: {
  nom: string;
  description: string;
  prix: number;
  quantite: number;
}) => {
  produits.value.push(produit);
};

const supprimerProduit = (index: number) => {
  produits.value.splice(index, 1);
};

const modifierProduit = ({
  index,
  produit,
}: {
  index: number;
  produit: { nom: string; description: string; prix: number; quantite: number };
}) => {
  produits.value[index] = produit;
};

// Source: ChatGPT
const dupliquerProduit = (index: number) => {
  const produitOriginal = produits.value[index];
  const nouveauProduit = {
    ...produitOriginal,
    nom: `${produitOriginal.nom} (copie)`,
  };
  produits.value.splice(index + 1, 0, nouveauProduit);
};
</script>

<template>
  <Entete />
  <ListeProduits
    :produits="produits"
    @ajouter-produit="ajouterProduit"
    @supprimer-produit="supprimerProduit"
    @modifier-produit="modifierProduit"
    @dupliquer-produit="dupliquerProduit"
  />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
