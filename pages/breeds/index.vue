<template>
  <div>
    <v-card>
      <v-card-title>
        <div style="display: inline">
          <p>List of breeds</p>
        </div>
        <v-spacer></v-spacer>
        <v-text-field v-model="searchInput" @click="setSortType('search')" label="Search" >

        </v-text-field>
        <v-spacer></v-spacer>
        <v-btn-toggle>
          <v-btn @click="setSortType('a-z')">
            a-z
          </v-btn>
          <v-btn @click="setSortType('z-a')">
            z-a
          </v-btn>
        </v-btn-toggle>
      </v-card-title>

      <v-list style="background: #242424">
        <v-list-item v-for="(breed,i) in SortedList" :key="i">
          <v-list-item-title>{{breed}}</v-list-item-title>
          <v-list-item-action><v-btn :to="'/breeds/'+breed">go to page</v-btn></v-list-item-action>
        </v-list-item>
      </v-list>
    </v-card>
  </div>
</template>

<script>
export default {
name: "breeds",
  data(){
    return {
        breeds:[],
        sortType:'none',
        searchInput:'',
    }
  },
  methods:{
    getBreeds(){
      this.$axios.$get("https://dog.ceo/api/breeds/list").then((res) => {
        this.breeds = res.message
      })
    },
    setSortType(type){
      this.sortType = type;
    }
  },
  mounted(){
    this.getBreeds()
  },
  computed: {
    SortedList: function (){
      switch (this.sortType){
        case "search":
          return this.breeds.filter(item => {
            return item.toLowerCase().indexOf(this.searchInput.toLowerCase()) > -1
          })
          break;
        case "a-z":
            return this.breeds.sort()
          break;
        case "z-a":
            return this.breeds.sort().reverse()
          break;
        default:
          return this.breeds
          break;
      }
    }
  },
}
</script>

<style scoped>

</style>
