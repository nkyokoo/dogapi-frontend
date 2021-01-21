<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
        <v-card>
          <v-img :src="infoCardIMG">

          </v-img>
          <v-card-title>
            Dog api
          </v-card-title>
          <v-card-text>
            This is a webapp for the dog api. The site can be found at <a href="https://dog.ceo/dog-api" target="_blank">https://dog.ceo/dog-api</a>
          </v-card-text>
        </v-card>
    </v-col>
  </v-row>
</template>

<script>

export default {
  components: {

  },
  data(){
    return {
      infoCardIMG:''
    }

  },
  methods:{
    async API_getRandomImage(){
      this.$axios.$get("https://dog.ceo/api/breeds/image/random").then((res) => {
        this.infoCardIMG = res.message
      })
    }
  },
  mounted() {
    this.API_getRandomImage()
  }
}
</script>
