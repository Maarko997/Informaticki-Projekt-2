<template>
  <v-row>
    <v-col class="mt-4 mb-2" cols="12">
      <v-subheader class="text-center font-weight-bold display-2">Popularno</v-subheader>
      <hr>
    </v-col>

    <v-col
      v-for="article in popularArticles"
      :key="article.id"
      cols="12"
      md="6"
      lg="4"
    >
      <ArticleCard
        :imageSrc="article.media[0]['media-metadata'][2].url"
        :title="article.title"
        :publishedDate="article.published_date"
        :abstract="article.abstract"
        :url="article.url"
      />
    </v-col>


    <v-col class="mt-4 mb-2" cols="12">
      <v-subheader class="text-center font-weight-bold display-2">Top priče</v-subheader>
      <hr>
    </v-col>

    <v-col
      v-for="storie in topStories"
      :key="storie.id"
      cols="12"
      md="6"
      lg="4"
    >
      <ArticleCard
        :imageSrc="storie.multimedia.length ? storie.multimedia[0].url : ''"
        :title="storie.title"
        :publishedDate="storie.published_date"
        :abstract="storie.abstract"
        :url="storie.url"
      />
    </v-col>
  </v-row>
</template>

<script>
import ArticleCard from '../components/ArticleCard.vue'

export default {
  name: 'HomeView',
  components: {
    ArticleCard
  },
  created() {
    this.getData();
  },
  data() {
    return {
      popularArticles: [],
      topStories: [],
      maxArticlesToShow: 6 
    }
  },
  methods: {
    getData() {
      const api = "https://api.nytimes.com/svc/mostpopular/v2/emailed/7.json";
      const api2 = "https://api.nytimes.com/svc/topstories/v2/arts.json";

      this.axios.get(api, {
        params: {
          'api-key': 'qAq0cVcFkOZWze3Mews5iD9W9etUc77j'
        }
      })
      .then((response) => {
        this.popularArticles = response.data.results.slice(0, this.maxArticlesToShow);
      });

      this.axios.get(api2, {
        params: {
          'api-key': 'qAq0cVcFkOZWze3Mews5iD9W9etUc77j'
        }
      })
      .then((response) => {
        this.topStories = response.data.results.slice(0, this.maxArticlesToShow);
      });
    }
  }
}
</script>
