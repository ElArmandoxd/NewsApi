<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>International news</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">International news</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-card v-for="n in news" :key="n">
          <img :src="n.urlToImage" alt="">
          <ion-card-header>
            <ion-card-subtitle>{{n.author}}</ion-card-subtitle>
            <ion-card-title>{{n.title}}</ion-card-title>
          </ion-card-header>

          <ion-card-content>
            {{n.content}}
          </ion-card-content>
          <a :href="n.url"><ion-button expand="block">Leer noticia completa</ion-button></a>
        </ion-card>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle, IonCardContent, IonButton } from '@ionic/vue';
import axios from 'axios';

export default  {
  name: 'Tab2',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonCard, IonCardHeader, IonCardSubtitle, IonCardTitle , IonCardContent, IonButton },
  data(){
    return{
      news: null
    }
  },
  created(){
    this.getNews();
  },
  methods:{
    getNews(){
      axios.get('https://newsapi.org/v2/everything?q=international&apiKey=75a3f87eb8d84e328a0664e73d30e96e')
      .then(response =>{
        this.news = response.data.articles;
        console.log(this.news);
      })
      .catch( error =>{
        console.log(error);
      });
    }
  }
}
</script>