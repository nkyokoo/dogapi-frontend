<template>
  <div>
    <v-card>
      <v-card-title>
        List of breeds
      </v-card-title>
      <v-list>
        <v-list-item v-for="(breed,i) in breeds" :key="i">
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
        breeds:[]
    }
  },
  methods:{
    getBreeds(){
      this.$axios.$get("https://dog.ceo/api/breeds/list").then((res) => {
        this.breeds = res.message
      })
    },
  },
  mounted(){
    this.getBreeds()
  }
}
</script>

<style scoped>

</style>
