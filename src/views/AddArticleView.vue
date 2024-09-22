<template>
  <v-container class="forma">
    <v-form ref="form" v-model="valid">
      <v-subheader class="text-center font-weight-bold display-2 naslov text-primary">Dodaj novi članak</v-subheader>
      <v-divider></v-divider>

      <v-text-field
        v-model="naslov"
        label="Naslov"
        :rules="[v => !!v || 'Naslov je obavezan']"
        outlined
        required
      ></v-text-field>

      <v-text-field
        v-model="datum_objave"
        label="Datum objave (YYYY-MM-DD)"
        :rules="[v => !!v || 'Datum objave je obavezan']"
        outlined
        required
      ></v-text-field>

      <v-text-field
        v-model="slika"
        label="URL slike"
        :rules="[v => !!v || 'URL slike je obavezan']"
        outlined
        required
      ></v-text-field>

      <v-textarea
        v-model="opis"
        label="Opis"
        :rules="[v => !!v || 'Opis je obavezan']"
        outlined
        required
      ></v-textarea>

      <v-text-field
        v-model="url"
        label="URL članka"
        :rules="[v => !!v || 'URL članka je obavezan']"
        outlined
        required
      ></v-text-field>

      <v-row>
        <v-col cols="12" lg="3">
          <v-btn @click="submitArticle" color="primary" dark large class="submit-btn">
          Dodaj članak
        </v-btn>
        </v-col>
        <v-col cols="12" lg="9">
          <v-alert 
            type="success"
            v-model="successAlert" 
            dismissible>
            Uspješno ste dodali novi članak!
          </v-alert>
        </v-col>
      </v-row>
    </v-form>
  </v-container>
</template>

<script>
export default {
  name: 'AddArticleView',
  data() {
    return {
      valid: false,
      naslov: '',
      datum_objave: '',
      slika: '',
      opis: '',
      url: '',
      successAlert: false
    };
  },
  methods: {
    submitArticle() {
      if (this.$refs.form.validate()) {
        const articleData = {
          naslov: this.naslov,
          datum_objave: this.datum_objave,
          slika: this.slika,
          opis: this.opis,
          url: this.url
        };

        this.axios.post('http://localhost:3000/clanci/dodaj', articleData)
          .then(() => {
            this.clearForm();
            this.successAlert = true;
          })
          .catch(error => {
            console.error('Došlo je do greške prilikom dodavanja članka:', error);
          });
      }
    },
    clearForm() {
      this.naslov = '';
      this.datum_objave = '';
      this.slika = '';
      this.opis = '';
      this.url = '';
    }
  }
};
</script>

<style scoped>
.forma {
  max-width: 70%;
  margin: 50px auto;
  padding: 40px;
  background-color: rgba(255, 255, 255, 0.9);
  border-radius: 10px;
  box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.3);
}

.submit-btn {
  margin-top: 20px;
  background-color: #3F51B5;
  font-weight: bold;
}

.v-text-field,
.v-textarea {
  margin-bottom: 20px;
}

.v-btn {
  border-radius: 8px;
}
</style>
