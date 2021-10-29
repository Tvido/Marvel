<template>
  <nav class="navbar navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand">MARVEL</a>
      <form class="d-flex">
        <input
          class="form-control me-2"
          type="search"
          placeholder="Search"
          aria-label="Search"
          v-model.trim="search"
          @input="changeSearch(search)"
        />
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form>
      <!-- <div id="theme-open" class="fas fa-bars"></div> -->
    </div>
  </nav>
</template>

<script>
export default {
  name: "AppHeader",
  props: ["changeSearch"],
  data() {
    return {
      search: "",
      };
  },
};
</script>

<style scoped></style>
