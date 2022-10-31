<template>
    <div class="list">
        <ul>
            <li v-for="(heroe, index) in heroes" :key="index" @click="setHeroesUrl(heroe.url)">
                <img :src="imageUrl + heroe.thumbnail.path + '.' + heroe.thumbnail.extension" :alt="heroe.name">
                <h3>{{ heroe.name }}</h3>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'ListHeroes',
        props: [
            "imageUrl",
            "apiUrl"
        ],
        data() {
            return {
                heroes: [],
                nextUrl: "",
                currentUrl: ""
            }
        },
        methods: {
            fetchRequision() {
                let req = new Request(this.currentUrl)
                fetch(req)
                    .then((resp) => {
                        return resp.json()
                    }) 
                    .then((characters) => {
                        this.nextUrl = characters.next
                        characters.data.results.forEach(heroe => {
                            this.heroes.push(heroe) 
                        })
                        console.log(characters)
                    })
                    .catch((error) => {
                        console.log(error)
                    })
            },
            next() {
                this.currentUrl = this.nextUrl
                this.fetchRequision()
            },
            setHeroesUrl(url) {
                this.$emit('setHeroesUrl', url)
            }
        },
        created() {
            this.currentUrl = this.apiUrl
            this.fetchRequision()
        }
    }
</script>

<style lang="scss">
    @import "../assets/variable.scss";

    .list {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;

        ul {
            display: flex;
            flex-wrap: wrap;
            margin: 10px;
            margin-top: 2rem;
            border-radius: 5px;
            justify-content: center;
        }

        li {
            width: 15%;
            margin: 20px;
            cursor: pointer;
            border: 1px solid #CCC;
            border-radius: 5px;
            text-transform: capitalize;
            letter-spacing: 3px;


            img {
                width: 100%;
                height: 100%;
            }
        }
    }
</style>