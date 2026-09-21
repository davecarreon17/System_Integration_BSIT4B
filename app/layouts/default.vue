<template>
  <v-app>
   
      
        <v-navigation-drawer
          expand-on-hover
          permanent
          rail
        >
          <v-list>
            <v-list-item
              prepend-avatar="https://randomuser.me/api/portraits/women/85.jpg"
              subtitle="sandra_a88@gmailcom"
              title="Sandra Adams"
            ></v-list-item>
          </v-list>

          <v-divider></v-divider>

          <v-list density="compact" nav>
            <v-list-item prepend-icon="mdi-folder" title="Dashboard" value="dashboard"></v-list-item>
            <v-list-item prepend-icon="mdi-account-multiple" title="Qr-Scanner" value="qr-scanner"></v-list-item>
            <v-list-item prepend-icon="mdi-star" title="Starred" value="starred"></v-list-item>
          </v-list>
        </v-navigation-drawer>
        <slot />
        <v-main style="height: 250px"></v-main>
    

        <v-app-bar>
  <template v-slot:prepend>
    <v-app-bar-nav-icon></v-app-bar-nav-icon>
  </template>

  <v-app-bar-title>Application Bar</v-app-bar-title>
</v-app-bar>

  </v-app>
</template>

<script lang="ts" setup>
const drawer = ref(true)

</script>

<style></style>