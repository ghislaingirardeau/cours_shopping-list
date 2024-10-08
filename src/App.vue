<template>
  <!-- HTML -->
   <!-- bind c'est pour ajouter des variables js dans une class -->
    <!-- class, utiliser pour le css -->
     <!-- id un identifiant unique pour une balise html -->
   <h1 v-bind:class="italic" :id="titleH1" @mouseover="showConsole" > 
    <!-- Dans les accolades, on mets les variables du script, c'est du javascript à l'intérieur -->
    {{ title.toUpperCase() }} </h1>

    <button type="button" @click="hideForm" >Afficher le formulaire</button>
    <div v-if="showForm">
      <div>
        <label for="label">Nom du fruit: </label>
        <input type="text" name="label" v-model="newItem">
      </div>
      <div>
        <label for="label">Quantité: </label>
        <input type="number" min="0" max="100" name="quantity" v-model="newQuantity" @keyup.enter="addItem">
      </div>

      <!-- Event: pour gérer les événements, les actions de l'utilisateur  -->
      <button type="button" @click="addItem">Add Item</button>
    </div>
    

   <ul>
    <!-- V for pour rendre chaque element d'une liste de array  -->
    <li v-for="item in fruits" :id="item.id" :class="italic">
      {{ item.name }}, quantité de : {{ item.quantity }}
    </li>
   </ul>

   <!-- vif vérifie la condition, si true affiche la balise <p> sinon ne le contruit pas -->
   <p>Le panier vide</p>
   
   
</template>

<script setup>
// JAVASCRIPT

import { ref } from 'vue'

console.log('hello')

const newItem = ref("")
const newQuantity = ref(0)
const showForm = ref(true)

const title = "Shopping List"
const italic = "titre-italic"
const titleH1 = "id-unique"

/* array / tableau c'est pour rendre une liste */
/* une liste d'objet dans un tableau */
const fruits = ref([
  {id:1, name: "Pomme", quantity: 5}, {id:2, name: "Poire", quantity: 2},
  {id:3, name: "Kiwi", quantity: 4}
])

/* FUNCTIONS */
// Des qu'on utilise ref(), il faut utiliser .value pour l'appeler
function addItem() {
  if(newItem.value.length < 3)  {
    return
  }
  fruits.value.push({
    name: newItem.value, 
    quantity: newQuantity.value,
    id: fruits.value.length + 1
  })
  newItem.value = ""
  newQuantity.value = 0
}

function showConsole() {
  console.log('mouseover');
}

function hideForm() {
  // toogle ! inverse la valeur du boolean
  showForm.value = !showForm.value
}



/* object c'est pour décrire quelque chose  */
// const voiture = {
//   marque: "peugeot",
//   couleur: 'bleu'
// }
// console.log(voiture.marque);
// console.log(fruits[0].name);

</script>

<style scoped>
/* CSS */
/* scoped => le css ne s'applique que sur app.vue */
.titre-italic {
  font-style: italic;
}


</style>
