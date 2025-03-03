<script setup lang="ts">
import { ref, defineProps, defineEmits, watch } from "vue";

const props = defineProps<{
  produit: {
    nom: string;
    prix: number;
    quantite: number;
    description: string;
  };
}>();

const emit = defineEmits(["annuler", "confirmer"]);

// Variables locales
const nom = ref(props.produit.nom);
const prix = ref(props.produit.prix);
const quantite = ref(props.produit.quantite);
const description = ref(props.produit.description);
const formValide = ref(false);

watch(props.produit, (nouveauProduit) => {
  nom.value = nouveauProduit.nom;
  prix.value = nouveauProduit.prix;
  quantite.value = nouveauProduit.quantite;
  description.value = nouveauProduit.description;
});

// Validation du formulaire
// SOURCE: ChatGPT
const verifierFormulaire = () => {
  formValide.value =
    nom.value.trim() !== "" && !isNaN(Number(prix.value)) && quantite.value > 0;
};

const confirmer = () => {
  if (formValide.value) {
    emit("confirmer", {
      nom: nom.value,
      prix: prix.value,
      quantite: quantite.value,
      description: description.value,
    });
  }
};
</script>

<template>
  <div class="modal-overlay">
    <div class="popup">
      <h2>Modifier le produit</h2>
      <form @submit.prevent="confirmer">
        <div class="mb-3">
          <label class="form-label">Nom du produit</label>
          <input
            v-model="nom"
            type="text"
            class="form-control"
            required
            @input="verifierFormulaire"
          />
        </div>
        <div class="mb-3">
          <label class="form-label">Prix</label>
          <input
            v-model="prix"
            type="number"
            step="0.01"
            class="form-control"
            required
            @input="verifierFormulaire"
          />
        </div>
        <div class="mb-3">
          <label class="form-label">Quantité</label>
          <input
            v-model="quantite"
            type="number"
            class="form-control"
            required
            @input="verifierFormulaire"
          />
        </div>
        <div class="mb-3">
          <label class="form-label">Description</label>
          <textarea
            v-model="description"
            class="form-control"
            required
            @input="verifierFormulaire"
          ></textarea>
        </div>
        <div class="actions">
          <button
            type="button"
            class="btn btn-secondary"
            @click="emit('annuler')"
          >
            Annuler
          </button>
          <button type="submit" class="btn btn-primary" :disabled="!formValide">
            Enregistrer
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}
.popup {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  width: 400px;
}
.actions {
  display: flex;
  justify-content: space-between;
  margin-top: 15px;
}
</style>
