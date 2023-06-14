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
  </div>
</template>

<style lang="scss" scoped></style>
