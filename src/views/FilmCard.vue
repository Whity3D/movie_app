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
        name: 'FilmCard',
        props: {
            filmList: Array
        }
    };
</script>