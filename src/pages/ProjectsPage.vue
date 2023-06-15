<script>
import axios from "axios";
import Mycard from "../components/Mycard.vue";
import { store } from "../store";
import Pagination from "../components/Pagination.vue";

export default {
  name: "ProjectsPage",
  data() {
    return {
      projects: [],
      currentPage: 1,
      lastPage: null,
      totalNumbProjects: 0,
      store,
    };
  },
  mounted() {
    this.getProjects();
  },
  methods: {
    getProjects(pageNumber = 1) {
      axios
        .get(`${store.myUrl}/api/projects`, {
          params: {
            page: pageNumber,
          },
        })
        .then((resp) => {
          console.log(resp);
          this.projects = resp.data.results.data;
          this.currentPage = resp.data.results.current_page;
          this.lastPage = resp.data.results.last_page;
          this.totalNumbProjects = resp.data.results.total;
        });
    },
  },
  components: { Mycard, Pagination },
};
</script>

<template>
  <div class="container">
    <h2 class="text-center my-3">LISTA DEI PROGETTI</h2>
    <div class="total text-center my-3 text-success">
      {{ totalNumbProjects }} PROGETTI
    </div>
    <div class="row row-cols-3 g-3">
      <div class="col" v-for="project in projects" :key="project.id">
        <Mycard :project="project" />
      </div>
    </div>
    <!-- PAGINATION -->
    <Pagination
      :currentPage="currentPage"
      :lastPage="lastPage"
      @changePage="getProjects"
    />
  </div>
</template>

<style lang="scss" scoped></style>
