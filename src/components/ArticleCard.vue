<template>
  <v-card 
    class="mb-3 card"
    :href="url"
    target="_blank"
    elevation="2"
  >
    <v-img
      :src="slika"
      class="card-img"
    ></v-img>
    <v-card-title>{{ naslov }}</v-card-title>
    <v-card-subtitle>
      <small class="text-body-secondary">{{ formattedDate }}</small>
    </v-card-subtitle>

    <v-card-text>{{ opis }}</v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'ArticleCard',
  props: {
    slika: {
      type: String,
      required: true
    },
    naslov: {
      type: String,
      required: true
    },
    datum_objave: {
      type: String,
      required: true
    },
    opis: {
      type: String,
      required: true
    },
    url: {  
      type: String,
      required: true
    }
  },
  computed: {
    formattedDate() {
      const date = new Date(this.datum_objave);
      return date.toLocaleDateString('hr-HR', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      });
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

.card-img {
  width: 100%;
  height: 100%;
  max-height: 250px; 
  object-fit: cover; 
}

</style>
