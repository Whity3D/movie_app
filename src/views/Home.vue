<template>
    <div class="home">
        <v-container fluid grid-list-md>
            <v-layout align-space-around row wrap fill-height>
                <v-flex xs12 sm6 md4 lg3 v-for="film in this.filmList" :key="film.id">
                    <v-card>
                        <v-card-media :src="'http://image.tmdb.org/t/p/w500' + film.poster_path"
                                      height="500"></v-card-media>
                        <v-card-title text-align-center>
                            <v-badge color="red">
                                <span slot="badge" v-if="film.adult">18+</span>
                                <span>
                                    <h3>{{ film.title }}</h3>
                                </span>
                            </v-badge>
                            <div>{{ film.overview }}</div>
                        </v-card-title>
                        <v-divider></v-divider>
                        <v-layout row wrap justify-space-around>
                            <v-chip v-for="genre in film.genre_ids"
                                    :key="genre"
                                    dark
                                    label
                                    color="cyan">{{ findGenre(genre) }}
                            </v-chip>
                        </v-layout>
                    </v-card>
                </v-flex>
            </v-layout>
        </v-container>
        <v-pagination color="cyan accent-2" v-model="params.page" :length="this.resObj.total_pages"
                      v-on:input="getFilmList"></v-pagination>
    </div>
</template>

<script>
  // @ is an alias to /src
  import HelloWorld from '@/components/HelloWorld.vue';
  import { API_KEY, MAIN_URL } from '@/global';

  export default {
    data: function () {
      return {
        genreList: [],
        filmList: [],
        resObj: {},
        params: {
          api_key: API_KEY,
          language: 'ru',
          page: 1,
        },
        baseUrl: '',
      };
    },
    methods: {
      findGenre: function (genre) {
        for (let i = 0; i < this.genreList.length - 1; i++) {
          if (this.genreList[i].id === genre) {
            return this.genreList[i].name;
          }
        }
      },
      getFilmList: function () {
        this.$http.get(MAIN_URL + 'movie/popular', { params: this.params }).then(res => {
          this.resObj = res.body;
          this.filmList = res.body.results;
        });
      },
    },
    created: function () {
      this.getFilmList();
      this.$http.get(MAIN_URL + 'configuration', { params: { api_key: this.params.api_key } }).then(res => {
        this.baseUrl = res.body.images.base_url + 'w500';
      });
      this.$http.get(MAIN_URL + 'genre/movie/list', { params: this.params }).then(res => {
        this.genreList = res.body.genres;
      });
    },
    name: 'home',
    components: {
      HelloWorld,
    },
  };
</script>

<style>
    .v-card {
        min-height: 100%;
    }
</style>
