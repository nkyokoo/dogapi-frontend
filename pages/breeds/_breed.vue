<template>
  <div>
    <v-card>
      <v-card-title>{{$route.params.breed}}</v-card-title>
      <v-row v-model="model">
        <v-col
          style="height: fit-content"
          v-for="(breedImage, i) in breedImages"
          :key="breedImage"
          :id="'image'+i"
        >
          <v-card
            style="height: fit-content"
          >
            <v-img :src="breedImage"></v-img>
          </v-card>
        </v-col>
      </v-row>

    </v-card>
  </div>

</template>

<script>
export default {
  name: "breed",
  data(){
    return{
       breedImages:[],
      model:true,
    }
  },
  methods:{
    getBreedImages(){
      this.$axios.$get(`https://dog.ceo/api/breed/${this.$route.params.breed}/images`).then((res) => {
         this.breedImages = res.message;
      })
    }
  },
  mounted(){
    this.getBreedImages();
  }
}
</script>

<style scoped>

</style>
