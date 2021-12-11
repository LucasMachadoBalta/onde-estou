<template>
  <ion-page>
    <ion-header>
        <ion-toolbar>
          <ion-title>Onde estou?</ion-title>
        </ion-toolbar>
    </ion-header>
    <ion-content>
      <div class='container'>
        <h2>Coordenadas</h2>
        <h3>{{ lat }}</h3>   
        <h3>{{ lon }}</h3>   
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import { Geolocation } from '@capacitor/geolocation';
export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar
  },
  data() {
    return {
      lat:0,
      lon:0
    }
  }
});
</script>

<style scoped>
.container {
  text-align: center;

}
</style>