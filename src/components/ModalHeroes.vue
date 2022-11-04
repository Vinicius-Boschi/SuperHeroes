<template>
    <div class="detail">
        <div class="detail__view" v-if="showModal">
            <div class="detail__image" v-if="heroe">
                <img :src="heroe.images.sm" :alt="heroe.name">
            </div>
            <div class="detail__card" v-if="heroe">
                <h2 class="detail__card-fullName">{{ heroe.biography.fullName }}</h2>
                <h2 class="detail__card-name">{{ heroe.name }}</h2>
                <div class="detail__appearance">
                    <ul class="detail__lists">
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
                            <span>{{ heroe.appearance.height[1] }}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-dumbbell"></i>
                            <span>{{ heroe.appearance.weight[1] }}</span>
                        </li>
                        <li class="detail__list">
                            <i class="fa-solid fa-eye"></i>
                            <span>{{ heroe.appearance.eyeColor}}</span>
                        </li>
                    </ul>
                </div>
                 <div class="detail__powerstats">
                    <h2 class="detail__title">PowerStats</h2>
                   <ul class="detail__ul">
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-shield-halved"></i>
                            <p>Intelligence:</p>
                            <span class="detail__bars" :style="{width: heroe.powerstats.intelligence + '%'}">{{ heroe.powerstats.intelligence }}%</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-shield-halved"></i>
                            <p>Strength:</p>
                            <span class="detail__bars" :style="{width: heroe.powerstats.strength + '%'}">{{ heroe.powerstats.strength }}%</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-shield-halved"></i>
                            <p>Speed:</p>
                            <span class="detail__bars" :style="{width: heroe.powerstats.speed + '%'}">{{ heroe.powerstats.speed }}%</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-shield-halved"></i>
                            <p>Durability:</p>
                            <span class="detail__bars" :style="{width: heroe.powerstats.durability + '%'}">{{ heroe.powerstats.durability }}%</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-shield-halved"></i>
                            <p>Power:</p>
                            <span class="detail__bars" :style="{width: heroe.powerstats.power + '%'}">{{ heroe.powerstats.power }}%</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-shield-halved"></i>
                            <p>Combat:</p>
                            <span class="detail__bars" :style="{width: heroe.powerstats.combat + '%'}">{{ heroe.powerstats.combat }}%</span>
                        </li>  
                   </ul>
                </div>
                <div class="detail__infos">
                    <h2 class="detail__title">Informations</h2>
                    <ul class="detail__content">
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-user"></i>
                            <p>AlterEgo:</p>
                            <span>{{ heroe.biography.alterEgos }}</span>
                        </li>
                        <li class="detail__powerlist break">
                            <i class="fa-solid fa-user"></i>
                            <p class="detail__break">Aliases:</p>
                            <span class="detail__aliase">{{ String(heroe.biography.aliases) }}</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-user"></i>
                            <p>Place of birth:</p>
                            <span>{{ heroe.biography.placeOfBirth }}</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-user"></i>
                            <p>First appearance:</p>
                            <span>{{ heroe.biography.firstAppearance }}</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-user"></i>
                            <p>Publisher:</p>
                            <span>{{ heroe.biography.publisher }}</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-user"></i>
                            <p>Good or Bad:</p>
                            <span>{{ heroe.biography.alignment }}</span>
                        </li>
                    </ul>
                </div>
                <div class="detail__jobs">
                    <h2 class="detail__title">Jobs</h2>
                    <ul class="detail__content">
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-briefcase"></i>
                            <p>Occupation:</p>
                            <span>{{ heroe.work.occupation }}</span>
                        </li>
                        <li class="detail__powerlist">
                            <i class="fa-solid fa-briefcase"></i>
                            <p>Base:</p>
                            <span>{{ heroe.work.base }}</span>
                        </li>
                    </ul>
                </div>
            </div>
            <h2 class="detail__error" v-else>No informations founded.</h2>
            <button class="detail__close" @click="closeModal">Close</button>
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
                window.addEventListener('click', (e) => {
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
    @import "../assets/scss/variable.scss";
    @import "../assets/scss/styles/modal.scss";
</style>