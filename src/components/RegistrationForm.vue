<script setup>
import { reactive, ref } from 'vue';

const form = reactive({
  nom: '',
  prenom: '',
  email: '',
  mdp: '',
});

const empty_state =ref(false);
const correct_format = ref(true);

const handle_regisration = () => {
  if(!form.nom || !form.prenom || !form.email || !form.mdp){
    empty_state.value = true
    return;
  }

  if(!form.email.endsWith('.com')){
    correct_format.value = false;
  }



  if(form.nom && form.prenom && form.email && form.mdp && form.email.endsWith('.com')){
    empty_state.value = false;

    window.alert("L'inscription est réussie");
  }


}
</script>

<template>

  <form @submit.prevent="handle_regisration">

    <label for="nom">Nom</label>
    <input v-model="form.nom" type="text" id="nom">
    <div  id="n_error" :class="['error_div',  empty_state ? '' : 'hidden']">Ce champ est requis</div>
    <br>

    <label for="prenom">Prénom</label>
    <input v-model="form.prenom" type="text" id="prenom">
    <div  id="n_error" :class="['error_div',  empty_state ? '' : 'hidden']">Ce champ est requis</div>
    <br>

    <label for="email">E-mail</label>
    <input v-model="form.email" type="email" id="email">
    <div v id="n_error" :class="['error_div',  empty_state ? '' : 'hidden']">Ce champ est requis</div>
    <div id="n_error" :class="['error_div',  correct_format? 'hidden' : '']">E-mail incorrecte</div>
    <br>


    <label for="mdp">Mot de passe</label>
    <input v-model="form.mdp" type="text" id="mdp">
    <div id="n_error" :class="['error_div',  empty_state ? '' : 'hidden']">Ce champ est requis</div>
    <br>

    <button type="submit">Soumettre</button>

  </form>
</template>

<style scoped>
.error_div{
  color: rgb(211, 8, 8);
}

.hidden{
  display: none;
}

</style>
