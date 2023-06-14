<script>
import axios from "axios";
import Mycard from "./components/Mycard.vue";
import { store } from "./store";

export default {
  data() {
    return {
      projects: [],
      currentPage: 1,
      lastPage: null,
      totalNumbProject: 0,
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
          this.totalNumbProject = resp.data.results.total;
        });
    },
  },
  components: { Mycard },
};
</script>

<template>
  <div class="container">
    <h2 class="text-center my-3">LISTA DEI PROGETTI</h2>
    <div class="total text-center my-3 text-success">
      {{ totalNumbProject }} PROGETTI
    </div>
    <div class="row row-cols-3 g-3">
      <div class="col" v-for="project in projects" :key="project.id">
        <Mycard :project="project" />
      </div>
    </div>
    <!-- PAGINATION -->
    <nav
      v-if="lastPage"
      aria-label="Page navigation example"
      class="my-3 d-flex justify-content-end"
    >
      <ul class="pagination">
        <li class="page-item" :class="{ disabled: currentPage === 1 }">
          <a
            @click.prevent="getProjects(currentPage - 1)"
            class="page-link"
            href="#"
            >Previous</a
          >
        </li>
        <li
          class="page-item"
          :class="{ active: pageNum === currentPage }"
          v-for="pageNum in lastPage"
        >
          <a @click.prevent="getProjects(pageNum)" class="page-link" href="#">{{
            pageNum
          }}</a>
        </li>
        <li class="page-item" :class="{ disabled: currentPage === lastPage }">
          <a
            @click.prevent="getProjects(currentPage + 1)"
            class="page-link"
            href="#"
            >Next</a
          >
        </li>
      </ul>
    </nav>
  </div>
</template>

<style lang="scss">
@use "./styles/general.scss" as *;
</style>
