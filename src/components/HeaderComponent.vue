<template>
    <header>
        <h1 class="text-center">Rick and Morty</h1>
        <select class="form-select" @change="$emit('statusSearch')" v-model="store.statusFilter">
                <option value="">All</option>
                <option value="alive">Alive</option>
                <option value="dead">Dead</option>
                <option value="unknown">Unknown</option>
        </select>
    </header>
</template>

<script>
import {store} from '../store.js';
    export default {
        name: 'HeaderComponent',
        data(){
            return {
               store
            }
        }
    }
</script>

<style lang="scss" scoped>

</style>