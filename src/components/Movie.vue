<template>
  <v-container v-if="loading">
    <div class="text-xs-center">
        <v-progress-circular
          indeterminate
          :size="150"
          :width="8"
          color="green"
        />
      </div>
  </v-container>
  <v-container v-else>
    <v-layout wrap>
      <v-flex xs12 mr-1 ml-1>
        <v-card>
          <v-img
            :src="singleMovie.Poster"
            aspect-ratio="2"
          ></v-img>
          <v-card-title primary-title>
            <div>
              <h2 class="headline mb-0">{{ singleMovie.Title }}</h2>
              <h3>Year:</h3>{{ singleMovie.Year }}
              <h3>Director:</h3>{{ singleMovie.Director }}
            </div>
          </v-card-title>
          <v-card-actions>
            <v-btn flat color="green" @click="back">back</v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import movieApi from '@/services/MovieApi';
export default {
  props: {
    id: {
      type: String,
      required: true,
    },
  },
  data () {
    return {
      singleMovie: '',
      loading: true,
    };
  },
  mounted () {
    movieApi.fetchSingleMovie(this.id)
      .then(response => {
        this.singleMovie = response;
        this.loading = false;
      })
      .catch(error => {
        console.log(error);
      });
  },
  methods: {
    back () {
      this.$router.push('/');
    },
  },
};
</script>

<style lang="stylus" scoped>
  .v-progress-circular
    margin 1rem
</style>
