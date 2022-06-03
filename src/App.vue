<template>
  <main>
    <Header />

    <Form :state="state" @search-Anime="SearchAnime" />

    <div class="results" v-if="state.search_results.length != 0">
      <ResultList :data="state.results" type="result" />
    </div>
  </main>
</template>

<script>
import { reactive, onMounted, computed } from "vue";
import Header from "./components/Header";
import Form from "./components/Form";
import ResultList from "./components/ResultList";

export default {
  components: {
    Header,
    Form,
    ResultList,
  },

  setup() {
    const state = reactive({
      my_anime: [],
      search_results: [],

      anime: computed(() => {
        return state.my_anime;
      }),

      results: computed(() => {
        return state.search_results;
      }),
    });

    // Functional Programming
    const SearchAnime = (obj) => {
      const url = `https://api.jikan.moe/v4/anime?q=${obj.querys}`;
      fetch(url)
        .then((res) => res.json())
        .then((data) => {
          state.search_results = data.data;
        });
    };

    const handleInput = (e) => {
      if (!e.target.value) {
        state.search_results = [];
      }
    };

    // Before Render
    onMounted(() => {
      state.my_anime = JSON.parse(localStorage.getItem("my_anime")) || [];
    });

    // Return template data
    return {
      Header,
      Form,
      ResultList,
      state,
      SearchAnime,
      handleInput,
    };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
}
body {
  background-color: #eee;
}
main {
  margin: 0 auto;
  max-width: 768px;
  padding: 1.5rem;
}
h1 {
  text-align: center;
  margin-bottom: 1.5rem;
}

.results {
  list-style: none;
  background-color: #fff;
  border-radius: 0.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  max-height: 480px;
  overflow-y: scroll;
  margin-bottom: 1.5rem;
}
.result {
  display: flex;
  margin: 1rem;
  padding: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  transition: 0.4s;
}
.result img {
  width: 100px;
  border-radius: 1rem;
  margin-right: 1rem;
}
.details {
  flex: 1 1 0%;
  display: flex;
  align-items: flex-start;
  flex-direction: column;
}
.details h3 {
  font-size: 1.25rem;
  margin-bottom: 0.5rem;
}
.details p {
  font-size: 0.875rem;
  margin-bottom: 1rem;
}
.details .button {
  margin-left: auto;
}
.flex-1 {
  display: block;
  flex: 1 1 0%;
}
.myanime h2 {
  color: #888;
  font-weight: 400;
  margin-bottom: 1.5rem;
}
.myanime {
  list-style: none;
}
.myanime .anime {
  display: flex;
  align-items: center;
  margin-bottom: 1.5rem;
  background-color: #fff;
  padding: 1rem;
  border-radius: 0.5rem;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
}
.anime img {
  width: 72px;
  height: 72px;
  object-fit: cover;
  border-radius: 1rem;
  margin-right: 1rem;
}
.anime h3 {
  color: #888;
  font-size: 1.125rem;
}
.anime .episodes {
  margin-right: 1rem;
  color: #888;
}
.anime .button:first-of-type {
  margin-right: 0.5rem;
}
.anime .button:last-of-type {
  margin-right: 0;
}
.button {
  appearance: none;
  outline: none;
  border: none;
  background: none;
  cursor: pointer;
  display: block;
  padding: 0.5rem 1rem;
  background-image: linear-gradient(to right, deeppink 50%, darkviolet 50%);
  background-size: 200%;
  color: white;
  font-size: 1.125rem;
  font-weight: bold;
  text-transform: uppercase;
  transition: 0.4s;
}
.button:hover {
  background-position: right;
}
</style>
