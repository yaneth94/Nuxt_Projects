<template>
    <div>
         <h1>Albums de la página</h1>
        <div v-for="album in albums" :key="album.id">
            <h3>{{album.title}}</h3>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import env from '../config/env'

export default {
    name: 'IndexPage',
    data(){
        return{
            albums: []
        }
    },
    created(){
        axios.get(`${env.endpoint}/albums`).then(response => {
            console.log(response.data)
            this.albums = response.data
        })
    }
}
</script>

<style scoped>

</style>