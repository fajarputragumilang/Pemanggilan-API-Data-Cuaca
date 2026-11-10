<template>
  <ion-page>

    <!--HEADER-->
    <ion-header>
      <ion-toolbar>
        <ion-title style="color:azure; text-align:center">Aplikas Data Cuaca</ion-title>
      </ion-toolbar>
    </ion-header>

    <!--MAIN CONTENT-->
    <ion-content class="ion-padding">
      <div style="text-align:center">

        <!--Button-->
        <ion-button @click="getData" style="text-align:center;">Get Data Speed Wind</ion-button>

        <!--MAIN CONTENT-->
        <div v-if="dataCuaca">
          <p>Lokasi Koordinat Cuaca     : lat {{ dataCupeaca.latitude }}</p>

          <!--tabel-->
          <table border="1" style="width:100%; border-collapse:collapse; text-align:center">
            <tr>
              <th>Speed Wind</th>
            </tr>

            <tr v-for="(waktu, i) in dataCuaca.hourly.time" :key="i">
              <td>{{ dataCuaca.hourly.wind_speed_10m[i]}}</td>
            </tr>
          </table>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {IonPage, IonTitle, IonHeader, IonToolbar, IonButton, IonContent} from '@ionic/vue';
import axios from 'axios';
import {defineComponent} from 'vue';

//Export DefineComponent
export default defineComponent({
  name: 'Tab1',
  data () {
    return {
      dataCuaca: null as any
    };
  },

  methods: {
    async getData() {
      try {
        const url = 'https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&past_days=10&hourly=temperature_2m,relative_humidity_2m,wind_speed_10m';
        const hasil = await axios.get(url);
        this.dataCuaca = hasil.data;
      } catch (error) {
        console.error("ERROR DATA GAGAL DI AMBIL", error);
      }
    }
  },


  //EXPORT components IONIC

  components: {
    IonPage,
    IonHeader,
    IonTitle,
    IonButton,
    IonContent,
    IonToolbar
  }
})
</script>