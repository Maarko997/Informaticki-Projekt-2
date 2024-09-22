<template>
  <v-row class="mb-5">
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

    <v-col>
      <v-text-field
        v-model="searchArticle"
        label="Pretraži članke"
        prepend-inner-icon="mdi-magnify"
        solo
        @input="filterArticles"
      ></v-text-field>

      <v-row v-if="filteredArticles.length">
        <v-col 
          v-for="article in paginatedArticles" 
          :key="article.id" 
          cols="12" 
          md="6" 
          lg="4"
          @contextmenu.prevent="openEditModal(article)"
        >
          <ArticleCard
            :slika="article.slika"
            :naslov="article.naslov"
            :datum_objave="article.datum_objave"
            :opis="article.opis"
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

      <v-dialog v-model="editDialog" max-width="500px">
        <v-card>
          <v-card-title class="text-h5">Uredi ili izbriši članak</v-card-title>
          <v-card-text>
            <v-form ref="editForm" v-model="validEditForm">
              <v-text-field
                v-model="editArticleData.naslov"
                label="Naslov"
                :rules="[v => !!v || 'Naslov je obavezan']"
                required
              ></v-text-field>

              <v-textarea
                v-model="editArticleData.opis"
                label="Opis"
                :rules="[v => !!v || 'Opis je obavezan']"
                required
              ></v-textarea>

              <v-text-field
                v-model="editArticleData.datum_objave"
                label="Datum objave (YYYY-MM-DD)"
                :rules="[v => !!v || 'Datum objave je obavezan']"
                required
              ></v-text-field>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-btn color="primary" @click="saveEditedArticle">Spremi</v-btn>
            <v-btn color="error" @click="deleteArticle">Izbriši</v-btn>
            <v-btn color="secondary" @click="closeEditModal">Odustani</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
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
  data() {
    return {
      articles: [],
      searchArticle: '',
      filteredArticles: [],
      paginatedArticles: [],
      perPage: 6,
      page: 1,
      editDialog: false,
      validEditForm: false,
      editArticleData: {
        id: '',
        naslov: '',
        opis: '',
        datum_objave: ''
      }
    }
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
    }
  },
  created() {
    this.fetchArticles();
  },
  methods: {
    fetchArticles() {
      const api = "http://localhost:3000/clanci/dohvati";
      this.axios
        .get(api)
        .then((response) => {
          this.articles = response.data;
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
        article.naslov.toLowerCase().includes(searchArticleLower)
      );
    },
    updatePaginatedArticles() {
      const start = (this.page - 1) * this.perPage;
      const end = this.page * this.perPage;
      this.paginatedArticles = this.filteredArticles.slice(start, end);
    },
    openEditModal(article) {
      this.editArticleData = { ...article }; 
      this.editDialog = true;
    },
    closeEditModal() {
      this.editDialog = false;
      this.editArticleData = { id: '', naslov: '', opis: '', datum_objave: '' };
    },
    saveEditedArticle() {
      if (this.$refs.editForm.validate()) {
        const api = `http://localhost:3000/clanci/uredi/${this.editArticleData.id}`;
        this.axios
          .put(api, this.editArticleData)
          .then(() => {
            this.editDialog = false;
            this.fetchArticles(); 
            alert('Članak je uspješno uređen!');
          })
          .catch((error) => {
            console.error('Došlo je do greške prilikom uređivanja članka:', error);
          });
      }
    },
    deleteArticle() {
      if (confirm('Jeste li sigurni da želite izbrisati ovaj članak?')) {
        const api = `http://localhost:3000/clanci/izbrisi/${this.editArticleData.id}`;
        this.axios
          .delete(api)
          .then(() => {
            this.editDialog = false;
            this.fetchArticles();
            alert('Članak je uspješno izbrisan!');
          })
          .catch((error) => {
            console.error('Došlo je do greške prilikom brisanja članka:', error);
          });
      }
    }
  }
}
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  height: 100%;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}
</style>
