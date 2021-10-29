<template>
  <div id="app">
    <app-header :changeSearch="changeSearch" />

    <div class="container">
      <h1 class="pt-3 pb-3">Персонажи Marvel</h1>
      <app-modal :character="character" />
      <spinner v-if="loading" />

      
      <h5 v-if="!searchCharacters.length && !loading">Не найдено...</h5>

      <div class="row">
        <div
          v-for="(el, id) in searchCharacters"
          :key="el.id"
          class="card mb-4"
          style="max-width: 340px;"
        >
          <div class="row g-0">
            <div class="col-md-4">
              <img
                :src="el.thumbnail"
                :alt="el.nameor"
                class="img-fluid rounded-start"
              />
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h5 class="card-title">{{ el.name }}</h5>
                <!-- Button trigger modal -->
                <button
                  type="button"
                  class="btn btn-primary mt-3"
                  data-bs-toggle="modal"
                  data-bs-target="#exampleModal"
                  @click="characterIndex = id"
                >
                  More
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Spinner from './components/Spinner';
import AppModal from './components/AppModal';
import AppHeader from './components/AppHeader';

export default {
  name: 'App',
  components: {
    AppHeader,
    AppModal,
    Spinner,
  },
  data() {
    return {
      loading: false,
      characters: [],
      characterIndex: 0,
      search: '',
    };
  },
  methods: {
    fetchCharacters: function() {
      return fetch('https://netology-api-marvel.herokuapp.com/characters')
        .then(res => res.json())
        .then(json => (this.characters = json));
    },
    changeSearch: function(value) {
      this.search = value;
    },
  },
  computed: {
    character: function() {
      return this.searchCharacters[this.characterIndex] || null;
    },
    searchCharacters: function() {
      const { characters, search } = this;
      return characters.filter(character => {
        return (
          character.name.toLowerCase().indexOf(search.toLowerCase()) !== -1
        );
      });
    },
  },
  async mounted() {
    this.loading = true;
    await this.fetchCharacters();
    this.loading = false;
  },
};
</script>

<style></style>
