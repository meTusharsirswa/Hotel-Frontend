<template>
    <div>
      <!------Sidebar-------->
  
      <v-navigation-drawer color="primary" v-model="Drawer" app>
        <v-divider></v-divider>
        <div class="pa-5">
          <!-- <v-img :src="require('@/assets/images/soulwin-logo.png')"></v-img> -->
        </div>
  
        <div>
          <v-list class="pa-6">
            <template v-for="(item, i) in sidebarMenu">
              <div :key="i">
                <LayoutSidebar :item="item" class="leftPadding" />
              </div>
            </template>
          </v-list>
        </div>
      </v-navigation-drawer>
  
      <v-app-bar color="primary" app height="70">
        <v-app-bar-nav-icon class="iconcolor white--text"
          variant="text"
          @click="Drawer = !Drawer"
        ></v-app-bar-nav-icon>
        <v-toolbar-title class="white--text">
         Welcome {{ $auth.user.first_name }}
          {{ $auth.user.last_name }}</v-toolbar-title
        >
        <v-spacer></v-spacer>
  
        <!-- <LayoutFullHeaderProfile /> -->
      </v-app-bar>
    </div>
  </template>
  
  <script>
  
  import LayoutSidebar from "@/components/dashboard/Sidebar.vue";
  
  export default {
    components: {
        LayoutSidebar,
      
    },
    data() {
      return {
        Drawer: true,
        toggleMini: false,
        sidebarMenu: [
          {
            title: "Dashboard",
            icon: "mdi-view-dashboard-outline",
            to: "/dashboard",
          },
          {
            title: "Questions",
            icon: "mdi-help-rhombus-outline",
            to: "/dashboard/questions",
          },
        ],
  
      };
    },
    computed: {
    },
  };
  </script>