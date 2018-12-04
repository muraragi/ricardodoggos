<template>
    <div class="content">
        <div class="breeds" v-if="!loading">
            <dogs :breeds="formattedBreeds"></dogs>
        </div>
        <Loader v-if="loading"></Loader>
        <button v-if="!loading" @click="getNewBreeds">Get New Breeds</button>
    </div> 
</template>

<script>
import axios from 'axios'
import Loader from './Loader'
import Dogs from './Dogs'
export default {
    name: 'Breeds',
    components: {
        Loader,
        Dogs
    },
    data() {
        return({
            breeds: [],
            loading: false,
            startValue: 0
        })
    },
    mounted() {
        this.fetchBreeds()
    },
    computed: {
        formattedBreeds() {
            if(!this.loading){
                const formattedBreeds = this.breeds.slice(this.startValue, this.startValue + 12)
                return formattedBreeds
            }
        }
    },
    methods: {
        fetchBreeds () {
            this.loading = true
            const baseURL = 'https://dog.ceo/api/breeds/'
            axios.request({
                baseURL,
                url: 'list/all',
                method: 'get'
            })
            .then(response => {
                this.breeds = Object.keys(response.data.message)
                this.loading = false
            })
        },
        getNewBreeds () {
            this.startValue += 10;
        }
    },
}
</script>

<style lang="scss" scoped>
    .content {
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    button {
        display: block;
        background: none;
        width: 200px;
        height: 50px;
        margin-top: 10px;
        font-size: 18px;
        color: black;
        border: 1px solid rgb(6, 6, 15);
        border-radius: 6px;
        cursor: pointer;
        transition: all .3s ease;
        &:hover {
            background: rgb(6, 6, 15);
            color: white;
        }
    }
</style>
