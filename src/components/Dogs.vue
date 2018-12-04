<template>
    <div class="dogs">
        <div class="dog" v-for="breed in breeds" @click="selectBreed(breed)" :ref="'breed'+breed">{{ formatName(breed) }}</div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'dogs',
    props: {
        breeds: {
            type: Array,
            default: () => []
        }
    },
    data () {
        return({
            currentBreed: '',
            chance: Number 
        })
    },
    methods: {
        formatName (breedName) {
            return breedName.charAt(0).toUpperCase() + breedName.slice(1)
        },
        async selectBreed (breed) {
            const response = await axios.get(`https://dog.ceo/api/breed/${breed}/images/random`)
            this.currentBreed = response.data.message
            let chosenDiv = this.$refs[`breed${breed}`][0]
            this.chance = Math.floor(Math.random() * (10 - 0)) + 0
            if(this.chance >= 7) {
                chosenDiv.style.backgroundImage = `url(https://i.kym-cdn.com/entries/icons/original/000/027/439/1486485831_ou-5qw.gif)`
                chosenDiv.innerText = `Ricardo`
            }
            else{
                chosenDiv.style.backgroundImage = `url(${this.currentBreed})`
                chosenDiv.innerText = this.formatName(breed)
            }
            chosenDiv.style.backgroundRepeat = `no-repeat`
            chosenDiv.style.backgroundSize = `cover`
            chosenDiv.style.color = `white`
        }
    },
}
</script>

<style lang="scss" scoped>
    .dogs {
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
        .dog {
            height: 300px;
            width: 400px;
            font-size: 22px;
            color: black;
            text-align: center;
            text-shadow: 5px 2px 20px rgba(0,0,0,0.73);
            line-height: 300px;
            margin-bottom: 10px;
            border: 1px solid rgb(6, 6, 15);
            transition: all .3s ease;
            cursor: pointer;
            &:hover {
                background: rgb(6, 6, 15);
                color: white;
            }
            &:focus,
            &:active {
               background: rgb(13, 13, 32);
               border-color: rgb(13, 13, 32);
            }
        }
    }
</style>
