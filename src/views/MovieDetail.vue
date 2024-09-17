<template>
<div class="movie-detail">

    <div class="header">
        
        <div class="overlap-banner">
            
            <img :src="movie.Poster" :alt="movie.Title + ' Poster'" class="poster-image">            

            <div class="actions">
                <button class="add-to-list-button">Add To List</button>
            </div>
        </div>
        <hr/>
        <div class="content">
            <h2>{{ movie.Title }}</h2>
            <p>{{ movie.Plot }}</p>
        </div>
        
    </div>

    <div class="detail">

    </div>
</div>

</template>


<script setup>
import { ref, onBeforeMount } from 'vue'
import {useRoute} from 'vue-router'
import env from '@/env';

const movie = ref({})
const route = useRoute()

onBeforeMount(() => {
   fetch(`http://www.omdbapi.com/?i=${route.params.id}&apikey=${env.apikey}&plot=full`)
   .then(res => res.json())
   .then(data => {
        movie.value = data
    })
})
</script>


<style lang="scss">
    .movie-detail{
        .featured-card{
            
            position: relative;
            width: 100%;
            height: 300px;

            .featured-image{
                display: block; 
                width: 100%;
                height: 100%;
                
                object-fit: cover;
                position: relative;
                z-index: 0;
                filter: blur(3px);
                border-radius: 0 0 8px 8px;
            }
        }
        .header{
            position: relative;
            
            .overlap-banner{
                display: flex;
                justify-content: center;
                align-items: center;
                gap: 16px;

                .poster-image{
                
                    width: clamp(200px, 20%, 500px);
                    z-index: 1;
                    border: 4px solid white;
                    border-radius: 4px;
                    box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2)
                }
                .add-to-list-button{
                    width: 100%;
                    max-width: 300px;
                    background-color: tomato;
                    padding: 16px;
                    border-radius: 8px;
                    color: white;
                    font-size: 16px;
                    
                    transition: 0.4s;

                    &:active{
                        background-color: #3B8070;
                    }
                }

            }
            hr{
                margin: 16px;
            }
            .content{
                h2{
                    width: 100%;
                    text-align: center;
                    color: white;
                }

                p{
                    background-color: #998484;
                    margin: 0 8px;
                    padding: 8px;
                }
            }
        }
        
    }
</style>