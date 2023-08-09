<template>
    <div>
      <v-app id="inspire">
        <Main />
        <v-main>
          <Nuxt />
        </v-main>
      </v-app>
    </div>
  </template>
    <script>
  import Main from "@/components/dashboard/Main.vue";
  
  export default {
    name: "dashboard",
    components: {
      Main,
    },
  };
  </script>
    