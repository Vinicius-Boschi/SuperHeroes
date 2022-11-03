<!-- <template>
    <div class="modal">
        <div class="modal__content" v-if="showModal">
            <div class="modal__image" v-if="heroe">
               <img :src="heroe.images.sm" :alt="heroe.name">
            </div>
            <div class="modal__card" v-if="heroe">
                <h1> {{ heroe.id}} - {{ heroe.name }}</h1>
            </div>
            <h1 class="modal__error" v-else>Nenhuma informação encontrada</h1>
            <button class="modal__close" @click="closeModal">Fechar</button>
        </div>
    </div>
</template> -->

<template>
    <div class="detail">
        <div class="detail__view" v-if="showModal">
            <div class="detail__image" v-if="heroe">
                <img :src="heroe.images.sm" :alt="heroe.name">
            </div>
            <div class="detail__card" v-if="heroe">
                <h2 class="detail__card-title">{{ heroe.name }}</h2>
                <div class="detail__powerstats">
                   <ul>
                        <li class="detail__list">
                            <i class="fa-solid fa-shield-halved">Inteligência:</i>
                            <span>{{ heroe.powerstats.intelligence }}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-shield-halved">Força:</i>
                            <span>{{ heroe.powerstats.strength }}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-shield-halved">Velocidade:</i>
                            <span>{{ heroe.powerstats.speed }}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-shield-halved">Durabilidade:</i>
                            <span>{{ heroe.powerstats.durability }}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-shield-halved">Poder:</i>
                            <span>{{ heroe.powerstats.power }}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-shield-halved">Combate:</i>
                            <span>{{ heroe.powerstats.combat }}</span>
                        </li>  
                   </ul>
                </div>
                <div class="detail__appearance">
                    <ul>
                        <li class="detail__list">
                            <i class="fa-solid fa-venus-mars"></i>
                            <span>{{ heroe.appearance.gender }}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-star"></i>
                            <span>{{ heroe.appearance.race}}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-scale-unbalanced-flip"></i>
                            <span>{{ heroe.appearance.height[1]}}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-dumbbell"></i>
                            <span>{{ heroe.appearance.weight[1]}}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-eye"></i>
                            <span>{{ heroe.appearance.eyeColor}}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-duotone fa-user-hair-long"></i>
                            <span>{{ heroe.appearance.hairColor}}</span>
                        </li>
                    </ul>
                </div>
            </div>
            <h2 class="detail__error" v-else>O pokémon não foi encontrado</h2>
            <button class="close" @click="closeModal">Fechar</button>
        </div>  
    </div>
</template>

<script> 
    export default {
        name: 'ModalHeroes',
        props: [
            "apiUrl"
        ],
        data() {
            return {
                showModal: false,
                heroe: {}
            }
        },
        methods: {
            fetchRequision() {
                document.querySelectorAll('[data-id]').forEach((el) => {
                    el.addEventListener('click', (e) => {
                        this.id = e.target.dataset.id
                        this.complementUrl = '/id/' + this.id + '.json'
                        let req = new Request(this.heroesUrl + this.complementUrl)
                        fetch(req)
                            .then((resp) => {
                                return resp.json()
                            }) 
                            .then((data) => {
                                this.heroe = data
                                this.showModal = true
                            })
                            .catch((error) => {
                                console.log(error)
                            })
                    })
                    
                })
            },
            closeModal() {
                this.$emit('closeModal')
            }
        },
        created() {
            this.heroesUrl = this.apiUrl
            this.fetchRequision()
        }
    }
</script>

<style lang="scss">
    @import "../assets/variable.scss";

    .detail {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        position: fixed;
        top: 0;
        left: 0;
        padding: 65px 10px 10px;
        width: 100%;
        height: 100vh;
        background: $black-two;    
        overflow: scroll;

        &__view {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            width: 100%;
            height: 54vw;
            position: relative;
            max-width: 510px;   
            background-color: $white;
            border-radius: 5px;
            box-shadow: 0 15px 30px $black, 0 10px 10px $black;   
        }

        &__image {
            position: absolute;
            top: -60px;
            width: 120px;
        }

        &__error {
            color: $white;
            font-size: 1.5rem;
            font-weight: 600;
            text-align: center;
            margin-top: 2rem;
        }
    }
</style>