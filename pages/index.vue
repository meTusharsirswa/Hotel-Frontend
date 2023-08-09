<template>
  <div class="mx-0">
    <Login />
    <Register />
  </div>
</template>

<script>
import Login from "./login/index.vue";
import Register from "./register/index.vue";

export default {
  components: {
    Login,
    Register,
  },
};
</script>
