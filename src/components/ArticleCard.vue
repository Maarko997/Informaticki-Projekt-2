<template>
  <v-card 
    class="mb-3 card"
    :href="url"
    target="_blank"
    elevation="2"
  >
    <v-img
      :src="imageSrc"
      class="card-img"
    ></v-img>
    <v-card-title>{{ title }}</v-card-title>
    <v-card-subtitle>
      <small class="text-body-secondary">{{ publishedDate }}</small>
    </v-card-subtitle>
    <v-card-text>{{ abstract }}</v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'ArticleCard',
  props: {
    imageSrc: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    publishedDate: {
      type: String,
      required: true
    },
    abstract: {
      type: String,
      required: true
    },
    url: {  
      type: String,
      required: true
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
