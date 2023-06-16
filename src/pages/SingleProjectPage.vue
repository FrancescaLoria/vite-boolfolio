<script>
import axios from "axios";
import { store } from "../store";

export default {
  name: "SingleProjectPage",
  data() {
    return {
      store,
      project: null,
      errorMesage: "",
    };
  },
  mounted() {
    const slug = this.$route.params.slug;
    axios.get(`${this.store.myUrl}/api/projects/${slug}`).then(
      (resp) => {
        // if (resp.data.success) {
        //   this.project = resp.data.results;
        // } else {
        //   this.errorMesage = resp.data.error;
        // }
        console.log(resp);
        this.post = resp.data.results;
      },
      (error) => {
        console.log(error.response.status);
        console.log(error.response.data);
        if (error.response.status === 404) {
          this.$router.push({ name: "not-found" });
        } else {
          this.errorMessage = "QUALCOSA E' ANDATO STORTO...";
        }
      }
    );
  },
  // methods: {
  //   goBack() {
  //     // this.$router.back();
  //     this.$router.go(-1);
  //   },
  // },
};
</script>

<template>
  <section class="container">
    <router-link :to="{ name: 'projects' }" class="btn btn-success mb-3"
      >Back</router-link
    >
    <div v-if="project">
      <h2>{{ project.title }}</h2>
      <div class="tags my-4">
        <div class="technology my-3">{{ project.type.name }}</div>
        <span v-for="(technology, index) in project.technologies"
          >{{ technology.name }}
          {{ index === project.technologies.length - 1 ? "" : "," }}</span
        >
      </div>
      <p>
        {{ project.content }}
      </p>
    </div>
    <div v-else-if="errorMesage" class="my-4">
      {{ errorMesage }}
    </div>
  </section>
</template>

<style lang="scss" scoped></style>
