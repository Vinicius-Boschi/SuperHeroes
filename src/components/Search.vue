<template>
  <form @submit.prevent="setHeroesUrl" @keyup="this.setHeroesUrl()">
    <input
      id="searchName"
      type="text"
      placeholder="Pesquise seu personagem"
      v-model="searchValue"
    />
    <button @click="setHeroesUrl">
      <i class="fa-solid fa-magnifying-glass"></i>
    </button>
  </form>
</template>

<script>
export default {
  name: "Search",
  props: ["apiUrl"],
  data() {
    return {
      searchValue: "",
    };
  },
  methods: {
    setHeroesUrl() {
      if (this.searchValue !== "") {
        // console.log(this.$emit("setHeroesUrl", this.apiUrl + this.searchValue))
        this.searchValue = ""
      }
      
      let input = document.getElementById("searchName").value
      input = input.toLowerCase()
      let url = this.apiUrl

      for (let i = 0; i < url.length; i++) {
        if(typeof url[i] === "string") {
          url[i].style.display = "none"
        } else {
          url[i].style.display = "list-item"
        }
      }
    },
  },
  mounted() {
    this.setHeroesUrl()
  },
}
</script>

<style lang="scss">
  @import "../assets/scss/variable.scss";
  @import "../assets/scss/styles/search.scss";
</style>