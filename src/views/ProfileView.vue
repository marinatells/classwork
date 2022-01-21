<template>
  <div>{{ user.name }} {{ currentId }}</div>
</template>

<script>
export default {
  data: () => ({
    currentId: null,
    user: {},
  }),

  methods: {
    loadUser() {
      this.axios
        .get("https://jsonplaceholder.typicode.com/users/" + this.currentId)
        .then((response) => {
          this.user = response.data;
        });
    },
  },

  watch: {
    $route() {
      this.currentId = this.$route.params.id;
      this.loadUser();
    },
  },

  mounted() {
    console.log("mounted");
    this.currentId = this.$route.params.id;
    this.loadUser();
  },
};
</script>
