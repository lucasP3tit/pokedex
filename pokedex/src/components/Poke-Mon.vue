<template>
    <div>
        <div class="card">
            <div class="card-image">
                <figure>
                <img v-show="isFront" :src="pokemon.front">
                <img v-show="!isFront" :src="pokemon.back" >
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                
                <div class="media-content">
                    <p class="title is-4">{{ num }}:{{ name | namePokeConfig }}</p>
                    <p class="subtitle is-6">{{ pokemon.type}}</p>
                </div>
                </div>

                <div class="content">
                    <button class="button is-medium" @click="changeImg">Mudar Sprite</button>
                </div>
            </div>
        </div>
        <hr>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    props:{
        name: String,
        url:  String,
        num: Number,
    },

    data(){
        return{
            isFront: true,
            pokemon:{
                type:"",
                front: "",
                back:""
            }
        }
        
    },

    methods:{
        changeImg(){
            this.isFront = !this.isFront;
        }
    },

    created(){
        axios.get(this.url).then(resp=>{
            this.pokemon.type = resp.data.types[0].type.name;
            this.pokemon.front = resp.data.sprites.front_default;
            this.pokemon.back = resp.data.sprites.back_default;
            console.log(this.pokemon)
        }).catch(err => console.log(err));
    },

    filters:{
        namePokeConfig: (name) => name.toUpperCase()
    }
}
</script>