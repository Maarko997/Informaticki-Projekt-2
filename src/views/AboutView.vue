<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <h1>O Nama</h1>
        <p>
          The New York Times je globalni lider u novinarstvu. Osnovan 1851. godine, Times pruža detaljne i vjerodostojne vijesti, analize i izvještaje iz cijelog svijeta. Sa sjedištem u New Yorku, The New York Times postao je sinonim za visokokvalitetno izvještavanje i istraživačko novinarstvo.
        </p>
        <p>
          Misija The New York Times-a je pomoći ljudima razumjeti svijet kroz nezavisne, visokokvalitetne i točne vijesti. S više od 1600 novinara u više od 160 zemalja, Times pokriva sve aspekte globalnih događaja, uključujući politiku, ekonomiju, kulturu, sport i znanost.
        </p>
        <p>
          Kroz povijest, The New York Times osvojio je više od 130 Pulitzerovih nagrada, najviše od svih novina na svijetu. Times nastavlja inovirati i prilagođavati se digitalnom dobu, nudeći vrhunsko novinarstvo putem svojih digitalnih platformi, aplikacija i tiskanih izdanja.
        </p>
      </v-col>

      <v-col cols="12" lg="6">
        <v-img
          src="https://cloudfront-us-east-2.images.arcpublishing.com/reuters/7EENTR3HFBMMRC3XV3PJAMVHCA.jpg"
          height="400px"
          alt="The New York Times Building"
        ></v-img>
      </v-col>

      <v-col cols="12" lg="6">
        <v-list>
          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-map-marker</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>The New York Times Company</v-list-item-title>
              <v-list-item-subtitle>620 Eighth Avenue, New York, NY 10018</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-clock-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>Osnovano</v-list-item-title>
              <v-list-item-subtitle>1851</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-newspaper-variant-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>Broj zaposlenika</v-list-item-title>
              <v-list-item-subtitle>Više od 4,700</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-trophy-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title>Pulitzerove nagrade</v-list-item-title>
              <v-list-item-subtitle>Više od 130</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'AboutView',
};
</script>

<style scoped>
h1 {
  margin-bottom: 24px;
}
p {
  margin-bottom: 16px;
}
</style>
