<script>
export default {
  name: "Mycard",
  props: {
    project: Object,
  },
  computed: {
    pwContent() {
      if (!this.project.content) {
        return "Nessun contenuto aggiunto";
      } else if (this.project.content.length > 150) {
        return this.project.content.substring(0, 150) + "...";
      } else {
        return this.project.content;
      }
    },
  },
};
</script>

<template>
  <div class="card p-3">
    <h4 class="title-card">TITOLO: {{ project.title }}</h4>
    <p class="content-card my-2">CONTENUTO: {{ pwContent }}</p>
    <p class="text-primary">
      <span v-if="project.type">{{ project.type.name }}</span>
      <span v-else>NESSUNA TIPOLOGIA</span>
    </p>
    <p class="text-success">
      <span v-if="project.technologies.length">
        <ul>
          <li v-for="technology in project.technologies" :key="technology.id">
            {{ technology.name }}
          </li>
        </ul>
      </span>
      <span v-else>NESSUNA TECNOLOGIA</span>
    </p>
    <router-link
      :to="{ name: 'single-project', params: { slug: project.slug } }"
      class="btn btn-primary"
      >Dettagli</router-link
    >
  </div>
</template>

<style lang="scss" scoped></style>
