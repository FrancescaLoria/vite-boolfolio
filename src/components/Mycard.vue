<script>
export default {
  name: "Mycard",
  props: {
    project: Object,
  },
};
</script>

<template>
  <div class="card p-3">
    <h4 class="title-card">TITOLO: {{ project.title }}</h4>
    <p class="content-card my-2">CONTENUTO: {{ project.content }}</p>
  </div>
</template>

<style lang="scss" scoped></style>
