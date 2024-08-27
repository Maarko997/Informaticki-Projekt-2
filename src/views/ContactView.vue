<template>
    <v-container>
      <v-row>
        <v-col cols="12" md="6">
          <h1>Kontaktirajte nas</h1>
          <p>
            Ako imate bilo kakva pitanja, slobodno nas kontaktirajte putem
            telefona, emaila ili ispunite kontakt formu.
          </p>
          <v-list>
            <v-list-item>
              <v-list-item-icon>
                <v-icon>mdi-map-marker</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title>Adresa</v-list-item-title>
                <v-list-item-subtitle>620 Eighth Avenue, New York, NY 10018</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
  
            <v-list-item>
              <v-list-item-icon>
                <v-icon>mdi-phone</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title>Telefon</v-list-item-title>
                <v-list-item-subtitle>800-698-4637</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
  
            <v-list-item>
              <v-list-item-icon>
                <v-icon>mdi-email</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title>Email</v-list-item-title>
                <v-list-item-subtitle>TheNYtimes@mail.com</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
  
          <v-btn color="primary" class="my-5" @click="dialog = true">
            Kontaktirajte nas putem forme
          </v-btn>

          <v-alert 
            type="success"
            v-model="successAlert" 
            dismissible>
            Uspješno ste poslali poruku!
          </v-alert>
        </v-col>
  
        <v-col cols="12" md="6">
          <v-img
            src="https://miro.medium.com/v2/resize:fit:1280/0*3ugnAu9VwlVbnQFb"
            height="400px"
          ></v-img>
        </v-col>
      </v-row>
  
      <v-dialog v-model="dialog" max-width="500px">
        <v-card>
          <v-card-title>
            <span class="headline">Kontakt Forma</span>
          </v-card-title>
          <v-card-text>
            <v-form>
              <v-text-field label="Ime" required></v-text-field>
              <v-text-field label="Email" required></v-text-field>
              <v-textarea label="Poruka" required></v-textarea>
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="dialog = false">
              Odustani
            </v-btn>
            <v-btn color="blue darken-1" text @click="submitForm">
              Pošalji
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-container>
  </template>
  
  <script>
  export default {
    data() {
      return {
        dialog: false,
        successAlert: false
      };
    },
    methods: {
      submitForm() {
        this.dialog = false;
        this.successAlert = true;
      },
    },
  };
  </script>
  
  <style scoped>
  h1 {
    margin-bottom: 16px;
  }
  </style>
  