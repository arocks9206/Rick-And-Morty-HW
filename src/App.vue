<template lang="html">
  <div>
   <h1>Ricky and Morty</h1>
   <div class="main-container">
     <character-list :characters='characters'></character-list>
     <character-detail v-if="selectedCharacter" :character="selectedCharacter"></character-detail>
   </div>
 </div>
</template>

<script>
import CharacterList from './components/CharacterList.vue';
import {eventBus} from './main.js';
import CharacterDetail from './components/CharacterDetail.vue';

export default {
  name: 'app',
  data() {
    return {
      characters: [],
      selectedCharacter: null
    };
  },
  mounted() {
    fetch('https://rickandmortyapi.com/api/character/')
    .then(response => response.json())
    .then(characters => this.characters = characters.results);

    eventBus.$on('character-selected', (character) => {
      this.selectedCharacter = character;
    })
  },
  components: {
   'character-list': CharacterList,
   'character-detail': CharacterDetail
 }
}
</script>

<style lang="css" scoped>
.main-container {
    display: flexl;
    justify-content: space-between;
  }
</style>
