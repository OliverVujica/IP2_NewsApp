<template>
    <div id="sve">
      <h2 style="text-align: center;">Stories by Section</h2>
      <br>
      <v-autocomplete @input="fetchTopStories"
        v-model="selectedSection"
        :items="sections"
        label="Select Section"
        clearable
        hide-no-data
      ></v-autocomplete>
      <v-container fluid v-if="displayedArticles.length > 0">
        <v-row>
          <v-col v-for="article in displayedArticles" :key="article.title" cols="12" sm="6" md="4">
            <v-card class="my-3">
              <v-img :src="article.imageUrl" height="200"></v-img>
              <v-card-title>{{ article.title }}</v-card-title>
              <v-card-text>{{ article.abstract }}</v-card-text>
              <v-card-actions>
                <v-btn text color="black" :href="article.url" target="_blank">Read More</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
      <p v-else></p>
      <v-pagination
        v-model="currentPage"
        :length="totalPages"
        @input="paginate"
        :prev-icon="prevIcon"
        :next-icon="nextIcon"
        color="primary"
      ></v-pagination>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        selectedSection: '',
        sections: [
            'Arts',
            'Business',
            'Sports',
            'Technology',
            'Science',
            'World',
            'Us',
            'Politics',
            'Magazine',
        ],
        articles: [],
        currentPage: 1,
        itemsPerPage: 9 
      };
    },
    computed: {
      totalPages() {
        return Math.ceil(this.articles.length / this.itemsPerPage);
      },
      displayedArticles() {
        const start = (this.currentPage - 1) * this.itemsPerPage;
        const end = start + this.itemsPerPage;
        return this.articles.slice(start, end).map(article => ({
          ...article,
          imageUrl: article.multimedia && article.multimedia.length > 0 ? article.multimedia[0].url : ''
        }));
      },
      prevIcon() {
        return this.$vuetify.rtl ? 'mdi-chevron-right' : 'mdi-chevron-left';
      },
      nextIcon() {
        return this.$vuetify.rtl ? 'mdi-chevron-left' : 'mdi-chevron-right';
      }
    },
    methods: {
      async fetchTopStories() {
        try {
          const response = await axios.get('https://api.nytimes.com/svc/topstories/v2/' + this.selectedSection + '.json', {
            params: {
              'api-key': '0EoubO7iGGZx3n4cvb2LyO6SnmNMssze'
            }
          });
          this.articles = response.data.results;
          this.currentPage = 1;
        } catch (error) {
          console.error(error);
        }
      },
      paginate(value) {
        this.currentPage = value;
      }
    }
  };
  </script>
  
  <style scoped>
    #sve {
        margin: 0 auto;
        width: 82%;
    }
  </style>
  
  