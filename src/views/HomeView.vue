<template>
  <v-row class="mb-5">
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

    <v-col cols="12">
      <v-parallax
        src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg"
      >
      <div class="d-flex flex-column fill-height justify-center align-center text-white">
        <h1 class="text-h4 font-weight-thin mb-4">
          Svijet Novosti
        </h1>
        <h4 class="subheading">
          Pronađite najbolje članke na jednom mjestu!
        </h4>
      </div>
      </v-parallax>
    </v-col>

    <v-col class="mt-4" cols="12" lg="5">
      <v-subheader class="text-center font-weight-bold display-2">Kategorije :</v-subheader>
    </v-col>

    <v-col class="mt-4" cols="12" lg="7">
      <v-select
        v-model="selectedCategory"
        :items="categories"
        outlined
        @change="getData"
      ></v-select>
    </v-col>

    <v-col
      v-for="article in articles"
      :key="article._id"
      cols="12"
      md="6"
      lg="4"
    >
      <ArticleCard
        :imageSrc="getImageUrl(article.multimedia)"
        :title="article.headline.main"
        :publishedDate="article.pub_date"
        :abstract="article.abstract"
        :url="article.web_url"
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
      articles:[],
      selectedCategory: 'Education', 
      categories: [
        'Arts', 'Automobiles', 'Books', 'Education',
        'Food', 'Health', 'Home & Garden', 'Lifestyle', 'Movies',
        'Music', 'Science', 'Sports', 'Technology', 'Travel'
      ]
    }
  },
  methods: {
    getData() {
      const api = "https://api.nytimes.com/svc/mostpopular/v2/emailed/7.json";
      const api2 = "https://api.nytimes.com/svc/search/v2/articlesearch.json";

      this.axios.get(api, {
        params: {
          'api-key': 'qAq0cVcFkOZWze3Mews5iD9W9etUc77j'
        }
      }).then((response) => {
          this.popularArticles = response.data.results.slice(0, 3);
      });

      this.axios.get(api2, {
        params: {
          'api-key': 'qAq0cVcFkOZWze3Mews5iD9W9etUc77j',
          'fq': `section_name:("${this.selectedCategory}")`,
          'sort': 'newest'
        }
      })
      .then((response) => {
        this.articles = response.data.response.docs.slice(0, 9);
      });
    },
    getImageUrl(multimedia) {
      if (multimedia.length) {
        const baseUrl = 'https://static01.nyt.com/';
        const imageUrl = multimedia[0].url;
        return baseUrl + imageUrl;
      }
      return '';
    }
  }
}
</script>


    