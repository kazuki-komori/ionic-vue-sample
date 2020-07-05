<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>Hello World</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <Alert />
    </ion-content>
  </div>
</template>
<script>
  import Alert from "./Alert";
  export default {
    components:{
      Alert
    }
  }
</script>
