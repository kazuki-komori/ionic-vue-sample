<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>Hello World</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <Alert />
      <router-link to="search">製品ページへ</router-link>
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
