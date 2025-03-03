<script setup lang="ts">
import { ref } from "vue";

const nom = ref("");
const description = ref("");
const prix = ref("");
const quantite = ref("");
const isValid = ref(false);

const emit = defineEmits(["ajouter-produit"]);

const validerFormulaire = () => {
  isValid.value =
    nom.value.trim() !== "" &&
    description.value.trim() !== "" &&
    parseFloat(prix.value) > 0 &&
    parseInt(quantite.value) > 0;
  return isValid.value;
};

// SOURCE: ChatGPT
const ajouterProduit = () => {
  if (validerFormulaire()) {
    emit("ajouter-produit", {
      nom: nom.value,
      description: description.value,
      prix: `${parseFloat(prix.value).toFixed(2)}`,
      quantite: parseInt(quantite.value),
    });

    nom.value = "";
    description.value = "";
    prix.value = "";
    quantite.value = "";
    isValid.value = false;
  }
};
</script>

<template>
  <form
    @submit.prevent="ajouterProduit"
    novalidate
    :class="{ 'was-validated': isValid }"
  >
    <h2>Ajouter un produit</h2>

    <div class="mb-3">
      <label for="nom" class="form-label">Nom du produit</label>
      <input
        placeholder="Piles AA Duracell"
        type="text"
        id="nom"
        v-model="nom"
        class="form-control"
        required
        :class="{ 'is-invalid': !nom && isValid, 'is-valid': nom }"
      />
      <div class="invalid-feedback">Veuillez entrer un nom valide.</div>
    </div>

    <div class="mb-3">
      <label for="description" class="form-label">Description du produit</label>
      <input
        placeholder="Piles alcalines"
        type="text"
        id="description"
        v-model="description"
        class="form-control"
        required
        :class="{
          'is-invalid': !description && isValid,
          'is-valid': description,
        }"
      />
      <div class="invalid-feedback">
        Veuillez entrer une description valide.
      </div>
    </div>

    <div class="mb-3">
      <label for="prix" class="form-label">Prix du produit</label>
      <input
        placeholder="20,69$"
        type="number"
        id="prix"
        v-model="prix"
        class="form-control"
        required
        min="0.01"
        step="0.01"
        :class="{
          'is-invalid': !prix || (parseFloat(prix) <= 0 && isValid),
          'is-valid': parseFloat(prix) > 0,
        }"
      />
      <div class="invalid-feedback">Veuillez entrer un prix valide.</div>
    </div>

    <div class="mb-3">
      <label for="quantite" class="form-label">Quantité en stock</label>
      <input
        placeholder="15"
        type="number"
        id="quantite"
        v-model="quantite"
        class="form-control"
        required
        min="1"
        step="1"
        :class="{
          'is-invalid': !quantite || (parseInt(quantite) <= 0 && isValid),
          'is-valid': parseInt(quantite) > 0,
        }"
      />
      <div class="invalid-feedback">Veuillez entrer une quantité valide.</div>
    </div>

    <button type="submit" class="btn btn-success">Ajouter</button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: 1rem;
  background-color: #e5e6e0;
  border-radius: 5px;
  box-shadow: 0 0 1rem #00000033;
}

form button {
  padding: 0.5rem;
  width: 6%;
  background-color: #3ec846;
  color: white;
  border: none;
  border-radius: 5px;
  transition: 0.5s;
  cursor: pointer;
}

form input {
  padding: 0.5rem;
  border: 1px solid #00000033;
  border-radius: 5px;
}

form button:hover {
  background-color: #2e9833;
  transition: 0.5s;
}
</style>
