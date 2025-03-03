<script setup lang="ts">
import { ref, computed, watch } from "vue";

import FormulaireAjout from "./FormulaireAjout.vue";
import ConfirmationSuppression from "./ConfirmationSuppression.vue";
import DetailsProduit from "./DetailsProduit.vue";
import BoutonModification from "./BoutonModification.vue";
import BoutonDetails from "./BoutonDetails.vue";
import BoutonSuppression from "./BoutonSuppression.vue";
import BoutonDuplication from "./BoutonDuplication.vue";
import FormulaireModification from "./FormulaireModification.vue";
import BarreRecherche from "./BarreRecherche.vue";
import AlerteStockCritique from "./AlerteStockCritique.vue";
import BoutonExportationCSV from "./BoutonExportationCSV.vue";

const props = defineProps<{
  produits: {
    nom: string;
    prix: number;
    quantite: number;
    description: string;
  }[];
}>();

const emit = defineEmits([
  "ajouter-produit",
  "supprimer-produit",
  "modifier-produit",
  "dupliquer-produit",
]);

// Fenêtre modal de confirmation de suppression
const produitASupprimer = ref<{ nom: string; index: number } | null>(null);

const demanderConfirmation = (nom: string, index: number) => {
  produitASupprimer.value = { nom, index };
};

const confirmerSuppression = () => {
  if (produitASupprimer.value !== null) {
    emit("supprimer-produit", produitASupprimer.value.index);
    produitASupprimer.value = null;
  }
};

const annulerSuppression = () => {
  produitASupprimer.value = null;
};

// Fenêtre modal des détails du produit
const produitSelectionne = ref<{
  nom: string;
  prix: number;
  quantite: number;
  description: string;
} | null>(null);

const ouvrirDetails = (produit: {
  nom: string;
  prix: number;
  quantite: number;
  description: string;
}) => {
  produitSelectionne.value = produit;
};

const fermerDetails = () => {
  produitSelectionne.value = null;
};

// Fenêtre modal de modification du produit
const produitAModifier = ref<{
  nom: string;
  prix: number;
  quantite: number;
  description: string;
  index: number;
} | null>(null);

const ouvrirModification = (
  produit: {
    nom: string;
    prix: number;
    quantite: number;
    description: string;
  },
  index: number
) => {
  produitAModifier.value = { ...produit, index };
};

const annulerModification = () => {
  produitAModifier.value = null;
};

const confirmerModification = (produitModifie: {
  nom: string;
  prix: string;
  quantite: number;
  description: string;
}) => {
  if (produitAModifier.value !== null) {
    emit("modifier-produit", {
      index: produitAModifier.value.index,
      produit: produitModifie,
    });
    produitAModifier.value = null;
  }
};

// Duplication de produits
const dupliquerProduit = (index: number) => {
  emit("dupliquer-produit", index);
};

// Recherche de produits
const recherche = ref("");

const mettreAJourRecherche = (texte: string) => {
  recherche.value = texte;
};

//SOURCE/AIDE: ChatGPT
const produitsFiltres = computed(() =>
  props.produits.filter((produit) =>
    produit.nom.toLowerCase().includes(recherche.value.toLowerCase())
  )
);

// Couleur de la quantité des produits
const couleurStock = (quantite: number) => {
  if (quantite <= 10) return "rouge";
  if (quantite <= 50) return "jaune";
  return "vert";
};

// Alerte de stock critique
const produitCritique = ref<{ nom: string } | null>(null);

watch(
  () => props.produits,
  (nouvelleListe) => {
    for (const produit of nouvelleListe) {
      if (produit.quantite <= 10) {
        produitCritique.value = { nom: produit.nom };
        break;
      }
    }
  },
  { deep: true }
);

const fermerAlerte = () => {
  produitCritique.value = null;
};
</script>

<template>
  <FormulaireAjout @ajouter-produit="emit('ajouter-produit', $event)" />
  <BarreRecherche @recherche="mettreAJourRecherche" />

  <div class="listeProduits">
    <div class="enteteListeProduits">
      <h2>Liste des produits</h2>
      <BoutonExportationCSV :produits="produitsFiltres" />
    </div>
    <table class="tableauProduits">
      <tr class="enteteTableau">
        <th>Nom</th>
        <th>Prix</th>
        <th>Quantité</th>
      </tr>
      <tr v-for="(produit, index) in produitsFiltres" :key="index">
        <td>{{ produit.nom }}</td>
        <td>{{ produit.prix }} $</td>
        <td :class="couleurStock(produit.quantite)">{{ produit.quantite }}</td>
        <BoutonDetails @click="ouvrirDetails(produit)" />
        <td>
          <BoutonModification @click="ouvrirModification(produit, index)" />
        </td>
        <td><BoutonDuplication @dupliquer="dupliquerProduit(index)" /></td>
        <BoutonSuppression @click="demanderConfirmation(produit.nom, index)" />
      </tr>
    </table>
  </div>

  <AlerteStockCritique
    v-if="produitCritique"
    :produitNom="produitCritique.nom"
    @fermer="fermerAlerte"
  />

  <ConfirmationSuppression
    v-if="produitASupprimer"
    :produitNom="produitASupprimer.nom"
    @confirmer="confirmerSuppression"
    @annuler="annulerSuppression"
  />

  <DetailsProduit
    v-if="produitSelectionne"
    :produit="produitSelectionne"
    @fermer="fermerDetails"
  />

  <FormulaireModification
    v-if="produitAModifier"
    :produit="produitAModifier"
    @annuler="annulerModification"
    @confirmer="confirmerModification"
  />
</template>

<style scoped>
.listeProduits {
  display: flex;
  margin-top: 10px;
  flex-direction: column;
  gap: 1rem;
  padding: 1rem;
  background-color: #e5e6e0;
  border-radius: 5px;
  box-shadow: 0 0 1rem #00000033;
}

.enteteListeProduits {
  display: flex;
  justify-content: space-between;
  margin: 0 0 1rem 0;
  align-items: center;
}

.rouge {
  color: #a90000;
  text-size-adjust: 5px;
}

.jaune {
  color: #c8b400;
  text-size-adjust: 5px;
}

.vert {
  color: #00c000;
  text-size-adjust: 5px;
}
</style>
