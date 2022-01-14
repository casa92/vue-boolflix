<template>
    <div class="single-card" @mouseenter="showDescription()" @mouseleave="hideDescription()">
        <div class="single-card-front">
            <div v-if="description.poster_path" class="img-back">
                <img :src="`https://image.tmdb.org/t/p/w342/${description.poster_path}`" alt="">
            </div>
            <div class="alternative-image" v-else>
                <img src="../assets/img/image-not-found.png" alt="">
            </div>
        </div>
        
        <div class="single-card-back" :class="{ show : itemInfo}">
            <div>Titolo: {{ description.title }} {{ description.name }}</div>
            <!-- <div>Titolo: {{ description.title ? description.title : description.name }}</div> -->
            <div>Titolo originale: {{ description.original_title }} {{ description.original_name }}</div>
            <div class="single-card-flag">
                Lingua:
                <!-- se la lingua è presente tra le bandiere a disposizione stampo la bandiera -->
                <div v-if="flagsIcon.includes(description.original_language)">
                    <img :src="require(`../assets/img/${description.original_language}.svg`)" alt="">
                </div>
                
                <div v-else>
                    {{ description.original_language }}
                </div>

            </div>
            <div>Voto: {{ description.vote_average }}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ItemCard",
    data: function() {
        return {
            flagsIcon: ['it', 'en', 'fr', 'de'],
            itemInfo: false
        };
    },
    props: {
        description: {},
    },
    methods: {
        showDescription() {
            this.itemInfo = true
        },
        hideDescription() {
            this.itemInfo = false
        }
    }
}
</script>

<style lang="scss" scoped>
    .single-card {
        margin: 1px;
        max-width: 342px;
        height: 510px;

        .alternative-image {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 510px;
            width: 342px;
            
            img {
                max-width: 342px;
                height: auto;
                width: 80%;
                
            }
        }
        .img-back {
            img {
                max-width: 342px;
            }
        }
        &-front {
            img {
                height: 510px;
            }
        }
        &-flag {
            img {
                width: 20px;
            }
        }
    }
</style>