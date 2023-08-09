<template>
    <!---Single Item-->
    <v-list-item
      :to="item.to"
      rounded
      class="mb-1"
      active-color="primary"
    >
      <!---If icon-->
      <template>
        <v-icon class="mr-2" color="iconcolor">{{ item.icon }}</v-icon>
      </template>
      <v-list-item-title class="white--text">{{ item.title }}</v-list-item-title>
    </v-list-item>
  </template>
  <script>
  export default {
    props: {
      item: {
        type: Object,
        required: false,
      },
    },
    data() {
      return {};
    },
  };
  </script>
  