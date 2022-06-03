<template>
  <form @submit.prevent="FormHandler">
    <input
      type="text"
      placeholder="Search for an anime..."
      v-model="formData.query"
    />
    <button type="submit" class="button">Search</button>
  </form>
</template>

<script>
import { reactive } from "vue";

export default {
  props: {
    state: Object,
  },

  setup(props, { emit }) {
    const formData = reactive({
      query: "",
    });

    function FormHandler() {
      emit("search-Anime", {
        querys: formData.query,
      });
      formData.query = "";
    }

    // Return template data
    return {
      FormHandler,
      formData,
    };
  },
};
</script>

<style scoped>
form {
  display: flex;
  max-width: 480px;
  margin: 0 auto 1.5rem;
}
form input {
  appearance: none;
  outline: none;
  border: none;
  background: white;
  display: block;
  color: #888;
  font-size: 1.125rem;
  padding: 0.5rem 1rem;
  width: 100%;
}
</style>
