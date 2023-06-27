<template>
    <v-card>
            <v-img
                :src="article.multimedia[0].url"
                height="200"
              ></v-img>
              <br>
              <h3 id="naslov"> {{ article.title }} </h3>
              <v-card-text>
                {{ article.abstract }}
              </v-card-text>
              <v-card-subtitle>
                {{ article.published_date }}, {{ article.byline }}
              </v-card-subtitle>
              <v-card-actions>
                <v-btn
                  color="black"
                  text
                  @click='toURL(article.url)'
                >
                  Read more
                </v-btn>
              </v-card-actions>
            </v-card>
</template>

<script>
  export default {
     props: ['article']
  }
</script>