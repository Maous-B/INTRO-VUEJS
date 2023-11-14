<script setup>
import {ref, computed} from 'vue';
const nouveauTheme = ref('')
const listeThemes = ref([])

let listeThemeIdentifiant = 0
let swap = false

const ajouteNouveauTheme = () => {
  listeThemes.value.push({
    id: listeThemeIdentifiant,
    effectue: false,
    contenu: nouveauTheme.value
  })
  nouveauTheme.value='';
  listeThemeIdentifiant++;
}

const supressionTheme = (theme) => {
  const index = listeThemes.value.findIndex(t => t.id === theme.id);
  if (index !== -1) {
    listeThemes.value.splice(index, 1);
  }

}

const basculeEtudie = (theme) => {
  theme.effectue = !theme.effectue
}

const toutBascule = () =>{
  for(let i = 0; i < listeThemes.value.length; i++){
    !swap ? (listeThemes.value[i].effectue = true) : (listeThemes.value[i].effectue = false)
  }
  !swap? swap = true: swap = false
}

const onEnter = () => {
  ajouteNouveauTheme()
}
const tachesEffectuees = computed(() => listeThemes.value.filter(theme => theme.effectue).length);
const tachesNonEffectuees = computed(() => listeThemes.value.filter(theme => !theme.effectue).length);

</script>

<template>
  <h1 class="text-center"> Liste de thèmes à étudier</h1>
  <div>
    <div>

      <input v-model="nouveauTheme" @keyup.enter="onEnter" name="nouveauTheme" type="text" placeholder="Nouveau thème...">
      <button @click="ajouteNouveauTheme">Ajouter un thème</button>
    </div>
    <ul>


      <li v-for="(theme, index) in listeThemes" :key="theme.id">
        <div>
          <p :class="{effectue: theme.effectue}"> {{theme.contenu}} <button @click="supressionTheme(theme)">Supprimer le thème</button> <button @click="basculeEtudie(theme)">Marquer comme fait</button>
          </p>
        </div>
      </li>
    </ul>
  </div>

  <p>Nombre de tâches effectuées : {{ tachesEffectuees }}</p>
  <p>Nombre de tâches non effectuées : {{ tachesNonEffectuees }}</p>
  <button @click="toutBascule">Tout basculer</button>
</template>

<style scoped>
.effectue{
  text-decoration: line-through;
}
</style>