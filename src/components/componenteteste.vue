<template>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">

  <div class="flex items-center justify-center min-h-screen bg-gray-100">
    <div class="favorite-games-list w-full max-w-lg p-8 bg-white rounded-lg shadow-lg">
      <h2 class="text-3xl font-bold mb-6 text-gray-800 text-center">Lista de Jogos Favoritos</h2>

      <div class="form mb-6">
        <input
          v-model="newGame.title"
          placeholder="Nome do Jogo"
          class="border border-gray-300 p-3 rounded-md w-full mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
        <input
          v-model="newGame.year"
          placeholder="Ano de Lançamento"
          type="number"
          class="border border-gray-300 p-3 rounded-md w-full mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
        <input
          v-model="newGame.genre"
          placeholder="Gênero"
          class="border border-gray-300 p-3 rounded-md w-full mb-4 focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
        <button
          @click="addGame"
          class="bg-blue-500 text-white font-semibold py-3 px-4 rounded-md hover:bg-blue-600 transition w-full"
        >
          Adicionar Jogo
        </button>
      </div>

      <div v-if="games.length === 0" class="text-gray-500 text-center">
        <p>Nenhum jogo cadastrado </p>
      </div>

      <div v-else class="overflow-y-auto max-h-64">
        <ul class="space-y-4">
          <li
            v-for="(game, index) in games"
            :key="index"
            class="flex justify-between items-center bg-gray-50 p-4 rounded-md shadow-sm"
          >
            <div>
              <strong class="text-lg text-gray-700">{{ game.title }}</strong>
              <span class="text-gray-500">({{ game.year }}) - Gênero: {{ game.genre }}</span>
            </div>
            <button
              @click="removeGame(index)"
              class="bg-red-500 text-white py-1 px-3 rounded-md hover:bg-red-600 transition"
            >
              Deletar
            </button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FavoriteGamesList',
  data() {
    return {
      newGame: {
        title: '',
        year: '',
        genre: '',
      },
      games: [],
    };
  },
  methods: {
    addGame() {
      if (this.newGame.title && this.newGame.year && this.newGame.genre) {
        this.games.push({ ...this.newGame });
        this.clearForm();
        this.scrollToBottom();
      } else {
        alert("preencha todos os campos");
      }
    },
    removeGame(index) {
      this.games.splice(index, 1);
    },
    clearForm() {
      this.newGame.title = '';
      this.newGame.year = '';
      this.newGame.genre = '';
    },
    scrollToBottom() {
      this.$nextTick(() => {
        const container = this.$el.querySelector('.overflow-y-auto');
        container.scrollTop = container.scrollHeight;
      });
    },
  },
};
</script>
