<template>
  
  <HeaderComponent @statusSearch="setParams"/>
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
        store,        
      }
    },
    methods:{
      /**
       *  setParams
       *  setta i parametri per la chiamata e inoltra la chiamata api
       *  passando i params
       */
      setParams(){
        const options=  {};
        if(this.store.statusFilter){
          options.params = {
            status: this.store.statusFilter
          }
        }
        this.getCharacters(options)  
      },
     /**
       * getCharacters methods
       * @param {*} opt 
       * chiamata api per recuperare i caratteri
       * accetta un oggetto opzionale contenente eventuali parametri
       * da passare in querystring
       * 
       */
      getCharacters(opt=null){
        //console.log(opt);
        this.store.loading = true;
        this.store.error.message = null;
        axios.get(this.store.apiUrl + this.store.endPoint.characters, opt).then((res) => {
          this.store.characters = res.data.results;
          this.store.total = res.data.info.count;
        }).catch((error) =>{
            // handle error
          //  console.log(error);
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