<template>
    <div class="single-card" @mouseenter="showDescription()" @mouseleave="hideDescription()">
        <div class="single-card-front">
            <div v-if="description.poster_path" class="img-back">
                <img :src="`https://image.tmdb.org/t/p/w342/${description.poster_path}`" alt="">
            </div>
            <div class="alternative-image" v-else>
                {{ description.title || description.name }}
                <img src="../assets/img/image-not-found.png" alt="">
            </div>
        </div>
        
        <div class="single-card-back">
            <div>Titolo: {{ description.title || description.name }}</div>
            <!-- <div>Titolo: {{ description.title ? description.title : description.name }}</div> -->
            <div>Titolo originale: {{ description.original_title || description.original_name }}</div>
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
            <div>Overview: {{ description.overview }}</div>
            <div>Voto: {{ Math.round(description.vote_average / 2) }}</div>
            <div>
                {{roundedVote()}}

                
                <!-- <div class="prova" v-for=""></div> -->
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ItemCard",
    data: function() {
        return {
            flagsIcon: ['it', 'en', 'fr', 'de'],
            itemInfo: false,
            totalStars: '',
        };
    },
    props: {
        description: {},
    },
    methods: {
        roundedVote() {
            let newNumber = Math.round(this.description.vote_average / 2);
            let stars = '';
            let i = 0;
            let singleStar = `<i class="fas fa-star"></i>`;
            while (i < newNumber) {
                stars += singleStar,
                i++
            };
            return stars
            
        },
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
        position: relative;

         &:hover .single-card-back{
                display: block;
            }

        .alternative-image {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            height: 510px;
            width: 342px;
            font-size: 20px;
            text-transform: uppercase;
            background-color: #000000;
            color: #fff;
            
            img {
                margin-top: 20px;
                max-width: 342px;
                height: auto;
                width: 25%;
                filter: invert(1);
                
            }
        }
        .img-back {
            img {
                max-width: 342px;
            }
        }
        &-front {
            z-index: 100;

            img {
                height: 510px;
            }
        }
        &-back {
            width: 100%;
            height: 100%;
            position: absolute;
            top: 0;
            left: 0;
            background-color: rgba($color: #000000, $alpha: 0.8);
            color: #fff;
            display: none;            

            .prova {
                border: 1px solid black;
                width: 5px;
                height: 5px;
                background-color: blanchedalmond;
            }
        }
        &-flag {
            img {
                width: 20px;
            }
        }

    }
</style>