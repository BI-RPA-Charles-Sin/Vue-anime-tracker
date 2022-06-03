<template>
  <h1>FavoriteList</h1>
  <div :class="type" v-for="(anime, index) in data" v-bind:key="{ index }">
    <img :src="anime.image" />
    <h3>{{ anime.title }}</h3>
    <div class="flex-1"></div>
    <span class="episodes"
      >{{ anime.watched_episodes }} / {{ anime.total_episodes }}</span
    >
    <!-- <button
      v-if="anime.total_episodes !== anime.watched_episodes"
      @click="increaseWatch(anime)"
      class="button"
    >
      +
    </button>
    <button
      v-if="anime.watched_episodes > 0"
      @click="decreaseWatch(anime)"
      class="button"
    >
      -
    </button> -->
  </div>
</template>

<script>
// import { reactive } from "vue";

export default {
  props: {
    type: String,
    data: Array,
  },

  //   setup(props) {
  //     // function FormHandler() {
  //     //   emit("search-Anime", {
  //     //     querys: formData.query,
  //     //   });
  //     //   formData.query = "";
  //     // }

  //     return {
  //     //   list,
  //     };
  //   },
};
</script>
