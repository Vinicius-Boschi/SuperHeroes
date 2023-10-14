<template>
  <div class="detail">
    <div class="detail__view" v-if="showModal">
      <div class="detail__image" v-if="heroe">
        <img :src="heroe.images.sm" :alt="heroe.name" />
      </div>
      <article class="detail__card" id="cardHeroes" v-if="heroe">
        <div class="detail__about">
          <div>
            <h2 class="detail__name">{{ heroe.name }}</h2>
          </div>
          <button class="detail__close" @click="closeModal">
            <i class="fa-solid fa-xmark"></i>
          </button>
        </div>
        <div class="detail__btns">
          <button class="detail__tab active" data-id="powerstats">PowerStats</button>
          <button class="detail__tab" data-id="biography">Biography</button>
          <button class="detail__tab" data-id="appearance">Appearance</button>
          <button class="detail__tab" data-id="connections">Connections</button>
        </div>
        <div class="detail__powerstats">
          <ul class="detail__ul active" id="powerstats">
            <li class="detail__infos">
             <div>
                <i class="fa-solid fa-shield-halved"></i>
                <span class="detail__info_name">Intelligence:</span>
             </div>
             <span
                class="detail__bars"
                :style="{ width: heroe.powerstats.intelligence }"
                >{{ heroe.powerstats.intelligence }}</span
              >
            </li>
            <li class="detail__infos">
              <div>
                <i class="fa-solid fa-shield-halved"></i>
                <span class="detail__info_name">Strength:</span>
              </div>
              <span
                class="detail__bars"
                :style="{ width: heroe.powerstats.strength }"
                >{{ heroe.powerstats.strength }}</span
              >
            </li>
            <li class="detail__infos">
              <div>
                <i class="fa-solid fa-shield-halved"></i>
                <span class="detail__info_name">Speed:</span>
              </div>
              <span
                class="detail__bars"
                :style="{ width: heroe.powerstats.speed }"
                >{{ heroe.powerstats.speed }}</span
              >
            </li>
            <li class="detail__infos">
              <div>
                <i class="fa-solid fa-shield-halved"></i>
                <span class="detail__info_name">Durability:</span>
              </div>
              <span
                class="detail__bars"
                :style="{ width: heroe.powerstats.durability }"
                >{{ heroe.powerstats.durability }}</span
              >
            </li>
            <li class="detail__infos">
              <div>
                <i class="fa-solid fa-shield-halved"></i>
                <span class="detail__info_name">Power:</span>
              </div>
              <span
                class="detail__bars"
                :style="{ width: heroe.powerstats.power }"
                >{{ heroe.powerstats.power }}</span
              >
            </li>
            <li class="detail__infos">
             <div>
                <i class="fa-solid fa-shield-halved"></i>
                <span class="detail__info_name">Combat:</span>
             </div>
              <span
                class="detail__bars"
                :style="{ width: heroe.powerstats.combat }"
                >{{ heroe.powerstats.combat }}</span
              >
            </li>
          </ul>
          <ul class="detail__ul" id="biography">
            <li class="detail__infos bio">
              <p class="detail__fullName">Full Name:</p>
              <span>{{ heroe.biography.fullName }}</span>
            </li>
            <li class="detail__infos bio">
              <p>Alter Egos:</p>
              <span>{{ heroe.biography.alterEgos }}</span>
            </li>
            <li class="detail__infos bio">
              <p>Aliases:</p>
              <span>{{ String(heroe.biography.aliases) }}</span>
            </li>
            <li class="detail__infos bio">
              <p>Place of Birth:</p>
              <span>{{ heroe.biography.placeOfBirth }}</span>
            </li>
            <li class="detail__infos bio">
              <p>First Appearance:</p>
              <span>{{ heroe.biography.firstAppearance }}</span>
            </li>
            <li class="detail__infos bio">
              <p>Publisher:</p>
              <span>{{ heroe.biography.publisher }}</span>
            </li>
            <li class="detail__infos bio">
              <p>Alignment:</p>
              <span>{{ heroe.biography.alignment }}</span>
            </li>
            <li class="detail__infos bio">
              <p>Occupation:</p>
              <span>{{ heroe.work.occupation }}</span>
            </li>
          </ul>
          <ul class="detail__ul" id="appearance">
            <li class="detail__infos">
              <div>
                <i class="fas fa-star"></i>
                <span class="detail__info_name">Gender:</span>
              </div>
              <span class="detail__appearance">{{ heroe.appearance.gender }}</span>
            </li>
            <li class="detail__infos">
              <div>
                <i class="fas fa-star"></i>
                <span class="detail__info_name">Race:</span>
              </div>
              <span class="detail__appearance">{{ heroe.appearance.race }}</span>
            </li>
            <li class="detail__infos">
              <div>
                <i class="fas fa-star"></i>
                <span class="detail__info_name">Height:</span>
              </div>
              <span class="detail__appearance">{{ heroe.appearance.height[1] }}</span>
            </li>
            <li class="detail__infos">
              <div>
                <i class="fas fa-star"></i>
                <span class="detail__info_name">Weight:</span>
              </div>
              <span class="detail__appearance">{{ heroe.appearance.weight[1] }}</span>
            </li>
            <li class="detail__infos">
              <div>
                <i class="fas fa-star"></i>
                <span class="detail__info_name">Eye Color:</span>
              </div>
              <span class="detail__appearance">{{ heroe.appearance.eyeColor }}</span>
            </li>
            <li class="detail__infos">
              <div>
                <i class="fas fa-star"></i>
                <span class="detail__info_name">Hair Color:</span>
              </div>
              <span class="detail__appearance">{{ heroe.appearance.hairColor }}</span>
            </li>
          </ul>
          <ul class="detail__ul" id="connections">
            <li class="detail__infos conect">
              <span class="detail__connections">Group Affiliation:</span>
              <span>{{ heroe.connections.groupAffiliation }}</span>
            </li>
            <li class="detail__infos conect">
              <span class="detail__connections">Relatives:</span>
              <span>{{ heroe.connections.relatives }}</span>
            </li>
          </ul>
        </div>
      </article>
      <h2 class="detail__error" v-else>No informations founded.</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalHeroes",
  props: ["apiUrl"],
  data() {
    return {
      showModal: false,
      heroe: {},
      changeUrl: "/id/"
    }
  },
  methods: {
    fetchRequision() {
      document.addEventListener("click", (e) => {
        this.id = e.target.dataset.id
        console.log(this.id)
        this.complementUrl = this.changeUrl + this.id + ".json"
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
    tabsBtns() {
      window.addEventListener("load", function () {
        const btns = document.querySelectorAll(".detail__tab")
        const card = document.querySelector(".detail")
        const lists = document.querySelectorAll(".detail__ul")

        card.addEventListener("click", (e) => {
          const id = e.target.dataset.id
          if (id) {
            btns.forEach((btn) => {
              btn.classList.remove("active")
              e.target.classList.add("active")
            })
            lists.forEach((list) => {
              list.classList.remove("active")
            })
            const element = document.getElementById(id)
            element.classList.add("active")
          }
        })
      })
    },
    closeModal() {
      this.$emit("closeModal")
    },
  },

  created() {
    this.heroesUrl = this.apiUrl
    this.fetchRequision()
    this.tabsBtns()
  },
}
</script>

<style lang="scss">
    @import "../assets/scss/variable.scss";
    @import "../assets/scss/styles/modal.scss";
</style>