<template>
    <div class="list">
        <div class="list__content">
            <img class="list__img" src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3d/DC_Comics_logo.svg/2048px-DC_Comics_logo.svg.png" alt="logo dc">
            <p>Bem vindo ao mundo da DC Comics.</p>
            <h2>Escolha seu personagem</h2>
        </div>
        <ul>
            <li class="list__li" v-for="(heroe, index) in heroes" :key="index" @click="setHeroesUrl(heroe.url)">
                <img class="list__image" :src="heroe.images.sm" :alt="heroe.name" :data-id='heroe.id'>
                <h3 class="list__title">{{ heroe.name }}</h3>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'ListHeroes',
        props: [
            "apiUrl"
        ],
        data() {
            return {
                heroes: [],
                currentUrl: "",
                complementUrl: "/all.json"
            }
        },
        methods: {
            fetchRequision() {
                let req = new Request(this.currentUrl + this.complementUrl)
                fetch(req)
                    .then((resp) => {
                        return resp.json()
                    }) 
                    .then((characters) => {
                        characters.forEach(heroe => {
                            this.heroes.push(heroe)
                        })
                    })
                    .catch((error) => {
                        console.log(error)
                    })
            },
            setHeroesUrl(url) {
                this.$emit("setHeroesUrl", url)
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
        color: $white;

        ul {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            margin-top: 2rem;
            gap: 2rem;
            text-align: center;

            @include phone {
                grid-template-columns: repeat(1, 1fr);
            }

            @include tablet {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        &__li {
            border-radius: 5px;
            text-transform: capitalize;
            letter-spacing: 3px;
            transition: all .3s linear;
        }

        &__image {
            width: 11.25rem;
            height: 17.5rem;
            border-radius: 30px;
            cursor: pointer;

            &:hover {
                transition: all .3s linear;
                opacity: .9;
                transform: translateY(-10px);
            }

            &:not(hover) {
                transition: all .3s linear;
            }
        }

        &__title {
            margin-top: 1rem;
            font-size: 1.25rem;
        }

        &__img {
            width: 3rem;
        }

        &__content {
            padding: 2rem;

            p {
                font-size: 14px;
                color: $white-two;
                margin-top: .5rem;
            }

            h2 {
                margin-top: 1rem;
                font-size: 2rem;
            }
        }
    }
</style>