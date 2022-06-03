<template>
  <h1>ResultList</h1>
  <div :class="type" v-for="(anime, index) in data" v-bind:key="{ index }">
    <img :src="anime.images.jpg.image_url" />
    <div class="details">
      <h3>{{ anime.title }}</h3>
      <p :title="anime.synopsis" v-if="anime.synopsis">
        {{ anime.synopsis.slice(0, 120) }}...
      </p>
      <span class="flex-1"></span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    type: String,
    data: Array,
  },
};
</script>
