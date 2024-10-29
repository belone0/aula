<template>
  <div class="movie-list">
    <h2>Cadastro de Filmes</h2>
    
    <form @submit.prevent="addMovie">
      <div>
        <label for="title">Título:</label>
        <input type="text" v-model="newMovie.title" id="title" placeholder="Título do filme" required />
      </div>
      
      <div>
        <label for="director">Diretor:</label>
        <input type="text" v-model="newMovie.director" id="director" placeholder="Diretor do filme" required />
      </div>
      
      <div>
        <label for="year">Ano de Lançamento:</label>
        <input type="number" v-model="newMovie.year" id="year" placeholder="Ano de lançamento" required />
      </div>

      <button type="submit">Cadastrar Filme</button>
    </form>

    <div v-if="movies.length === 0" class="empty-message">
      <p>Nenhum filme cadastrado.</p>
    </div>

    <ul v-else>
      <li v-for="(movie, index) in movies" :key="index">
        <strong>{{ movie.title }}</strong> - {{ movie.director }} ({{ movie.year }})
        <button @click="removeMovie(index)">Deletar</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newMovie: {
        title: '',
        director: '',
        year: ''
      },
      movies: []
    };
  },
  methods: {
    addMovie() {

      if (!this.newMovie.title || !this.newMovie.director || !this.newMovie.year) {
        alert("Por favor, preencha todos os campos.");
        return;
      }

      this.movies.push({ ...this.newMovie });

      this.newMovie = { title: '', director: '', year: '' };
    },
    removeMovie(index) {
      this.movies.splice(index, 1);
    }
  }
};
</script>

<style scoped>
.movie-list {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
}
form div {
  margin-bottom: 10px;
}
button {
  margin-top: 10px;
}
.empty-message {
  color: #999;
  font-style: italic;
}
</style>