<template>
  <v-container>
    <v-subheader class="text-center font-weight-bold display-2">Top novosti iz svijeta</v-subheader>
    <hr />

    <v-text-field
      v-model="searchArticle"
      label="Pretraži članke"
      prepend-inner-icon="mdi-magnify"
      solo
      @input="filterArticles"
    ></v-text-field>

    <v-row v-if="filteredArticles.length">
      <v-col v-for="article in paginatedArticles" 
        :key="article.id" 
        cols="12" 
        md="6" 
        lg="4">
        <ArticleCard
          :imageSrc="article.multimedia.length ? article.multimedia[0].url : ''"
          :title="article.title"
          :publishedDate="article.published_date"
          :abstract="article.abstract"
          :url="article.url"
        />
      </v-col>
    </v-row>

    <v-row v-else>
      <v-col cols="12">
        <p>Nema članaka za prikaz.</p>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12">
        <v-pagination
          v-model="page"
          :length="totalPages"
          @input="updatePaginatedArticles"
          rounded="circle"
        ></v-pagination>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import ArticleCard from '@/components/ArticleCard.vue';

export default {
  name: 'WorldArticleView',
  components: {
    ArticleCard,
  },
  data() {
    return {
      searchArticle: '',
      articles: [],
      filteredArticles: [],
      paginatedArticles: [],
      perPage: 6,
      page: 1,
    };
  },
  watch: {
    filteredArticles() {
      this.page = 1;  
      this.updatePaginatedArticles();
    },
    page() {
      this.updatePaginatedArticles();
    }
  },
  computed: {
    totalPages() {
      return Math.ceil(this.filteredArticles.length / this.perPage);
    },
  },
  created() {
    this.fetchArticles();
  },
  methods: {
    fetchArticles() {
      const api = `https://api.nytimes.com/svc/topstories/v2/world.json`;

      this.axios
        .get(api, {
          params: {
            'api-key': 'qAq0cVcFkOZWze3Mews5iD9W9etUc77j',
          },
        })
        .then((response) => {
          this.articles = response.data.results;
          this.filteredArticles = this.articles;
          this.updatePaginatedArticles();
        })
        .catch((error) => {
          console.error('There was an error fetching the articles:', error);
        });
    },
    filterArticles() {
      const searchArticleLower = this.searchArticle.toLowerCase();
      this.filteredArticles = this.articles.filter((article) =>
        article.title.toLowerCase().includes(searchArticleLower)
      );
    },
    updatePaginatedArticles() {
      const start = (this.page - 1) * this.perPage;
      const end = this.page * this.perPage;
      this.paginatedArticles = this.filteredArticles.slice(start, end);
    },
  },
};
</script>