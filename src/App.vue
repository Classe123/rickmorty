<template>
  <HeaderComponent />
  <MainComponent />
</template>

<script>
import {store} from './store.js';
import axios from 'axios';
import HeaderComponent from './components/HeaderComponent.vue';
import MainComponent from './components/MainComponent.vue';
  export default {
    name: 'App',
    components:{
      HeaderComponent,
      MainComponent
    },
    data(){
      return {
        store
      }
    },
    methods:{
      getCharacters(){
        this.store.loading = true;
        this.store.error.message = null;
        axios.get(this.store.apiUrl + this.store.endPoint.characters).then((res) => {
          this.store.characters = res.data.results;
          this.store.total = res.data.info.count;
          //this.store.loading = false;
        }).catch((error) =>{
            // handle error
           console.log(error);
           this.store.error.message = error.message;
        }).finally(() =>{
          this.store.loading = false;
        });
      }
    },
    created(){
      this.getCharacters();
    }
  }
</script>

<style lang="scss" scoped>

</style>