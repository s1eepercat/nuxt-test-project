<template>
  <section>
    <h1>{{title}}</h1>
    <ul>
      <li v-for="user of users" :key="user.id">
        <a href="#" @click.prevent="openUser(user)">{{user.name}}</a>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  // async asyncData({ $axios }) {
  //   const users = await $axios.$get(
  //     "https://jsonplaceholder.typicode.com/users"
  //   );
  //   return { users };
  // },
  async fetch({ store }) {
    if (store.getters["users/users"].length === 0) {
      await store.dispatch("users/fetch");
    }
  },
  computed: {
    users() {
      return this.$store.getters["users/users"];
    }
  },
  data() {
    return {
      title: "User page"
    };
  },
  methods: {
    openUser(user) {
      this.$router.push("/users/" + user.id);
    }
  }
};
</script>