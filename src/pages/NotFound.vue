<script>
export default {
  name: "NotFound",
  methods: {
    goBack() {
      this.$router.go(-1);
    },
  },
};
</script>

<template>
  <div class="container">
    <h2 class="text-center my-5">La pagina che stai cercando non esiste.</h2>
    <div>
      <router-link :to="{ name: 'home' }" class="btn btn-success"
        >Vai alla home</router-link
      >
      <a @click.prevent="goBack" class="btn btn-warning ms-2" href=""
        >Torna indietro</a
      >
    </div>
  </div>
</template>
