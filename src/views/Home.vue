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
        <h3>{{ latitude }}</h3>   
        <h3>{{ longitude }}</h3>
        <ion-button @click="buscaCidade()">Onde Estou?</ion-button>
        <h3>{{ cidade }}</h3>   
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButton } from '@ionic/vue';
import { defineComponent } from 'vue';
import { Geolocation } from '@capacitor/geolocation';
import { Http } from '@capacitor-community/http';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButton
  },
  data() {
    return {
      latitude:0,
      longitude:0,
      cidade: ""
    }
  },
  ionViewWillEnter(){
    this.printCurrentPosition();
  },
  methods: {
    printCurrentPosition: async function() {
      const coordinates = await Geolocation.getCurrentPosition();
      console.log('Current position:', coordinates);

      this.latitude = coordinates.coords.latitude;
      this.longitude = coordinates.coords.longitude;
    },
    buscaCidade: async function() {
      const ACCESS_KEY = "c5b79f5a379a87709c90ca73a8e3b119";
      const url = "http://api.positionstack.com/v1/reverse?access_key=" + ACCESS_KEY + "&query=" + this.latitude + "," + this.longitude;
      const options = {
        url: url
      };
      const response = await Http.get(options);
      console.log('resposta recebida: ', response);
      this.cidade = response.data.data[0].locality + ', ' + response.data.data[0].region_code;
    }
    
  }

});
</script>

<style scoped>
.container {
  text-align: center;

}
</style>