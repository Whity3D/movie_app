<template>
  <v-card>
    <v-card-media :src="this.baseUrl + this.filmList[0].poster_path" height="500"></v-card-media>
    <v-card-title>
      <h3>{{ this.filmList[0].title }}</h3>
      <div>{{ this.filmList[0].overview }}</div>
    </v-card-title>
    <v-layout row justify-space-around>
      <div v-for="genre in this.filmList[0].genre_ids">
        <v-chip outline color="primary">{{ genre }}</v-chip>
      </div>
    </v-layout>
  </v-card>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    filmList: Array,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
