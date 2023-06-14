<script>
import axios from "axios";
import Mycard from "./components/Mycard.vue";
import { store } from "./store";

export default {
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    this.getProjects();
  },
  methods: {
    getProjects() {
      axios.get(`${store.myUrl}/api/projects`).then((resp) => {
        this.projects = resp.data.results;
      });
    },
  },
  components: { Mycard },
};
</script>

<template>
  <div class="container">
    <h2 class="text-center my-3">LISTA DEI PROGETTI</h2>
    <div class="row row-cols-3 g-3">
      <div class="col" v-for="project in projects" :key="project.id">
        <Mycard :project="project" />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
@use "./styles/general.scss" as *;
</style>
