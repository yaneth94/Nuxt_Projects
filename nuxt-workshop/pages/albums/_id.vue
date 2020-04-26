<template>
  <div class="container">
    <header>
        <nuxt-link to="/">Regresar</nuxt-link>
    <h1 class="title ">{{album.title}}</h1>
    </header>
    <div class="columns is-multiline">
        <div class="column is-one-quarter" v-for="photo in photos" :key="photo.id">
            <img :src="photo.url" :alt="photo.title">
        </div>
    </div>
  </div>
</template>

<script>
import router from 'vue-router';
import axios from 'axios';
import env from '@/config/env'

export default {
    name: 'AlbumIndvPage',
    data(){
        return{
            album: {},
            photos: []
        }
    },
    created: async function (){
        
        //console.log(this.$route); aqui esta toda la infor
        let albumId = this.$route.params.id;
        let albumResponse = await axios.get(`${env.endpoint}/albums/${albumId}`);
        this.album= albumResponse.data;
        let photosResponse = await axios.get(`${env.endpoint}/albums/${albumId}/photos`);
        this.photos = photosResponse.data;
         /*axios.get(`${env.endpoint}/albums/${albumId}`).then(response => {
            this.album = response.data;
        })
        axios.get(`${env.endpoint}/albums/${albumId}/photos`).then(response => {
            this.photos= response.data;
        })*/
    }
}
</script>

<style scoped>
.header{
    margin-top: 1em;
    margin-bottom: .5em;
}
.container{
    text-align: center;
}   
</style>