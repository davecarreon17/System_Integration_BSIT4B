<template>
  <div class="mx-auto d-flex justify-center align-center" style="height: 90vh;">
    <v-card>
      <v-card-text>
      <!-- Show QR Scanner  -->
      <video class="qr-video"></video>
        <!-- Start Scanner -->
          <v-btn color="green" block> Start Scanner</v-btn>
         
        <!-- Stop Scanner -->
          <v-btn color="red" class="mt-5" block> StopScanner</v-btn>
      </v-card-text>
    </v-card>
  </div>
</template>

<script lang="ts" setup>

</script>

<style scoped>
.qr-video {
   width:100%;
  max-width: 400px;
  border-radius: 12px;
  background: black;}

</style>