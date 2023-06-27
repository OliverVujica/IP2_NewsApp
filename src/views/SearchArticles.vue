<template>
    <v-container>
      <r-row>
        <r-col>
          <h2 style="text-align: center;">You can search articles by headline here</h2>
           <br>
        </r-col>
      </r-row>
          <v-row>
                <v-col>
                    <v-text-field
                        v-model="searchTerm"
                        type="text"
                        placeholder="Search for articles"
                ></v-text-field>
                <v-btn
                    color="black"
                    text
                    @click="searchArticles"
                >   Click to Search
                </v-btn>
                </v-col>
            </v-row>
        <v-row>
            <v-col
              v-for="article in articles" :key="article.id"
                cols="3"
                sm="3"
            >
              <v-card height="420">
                <h3 id="naslov"> {{ article.headline.main }} </h3>
                <v-card-text>
                  {{ article.snippet }}
                </v-card-text>
                <v-card-subtitle>
                  {{ article.pub_date }}, {{ article.byline.original }}
                </v-card-subtitle>
                <v-card-actions>
                  <v-btn
                    color="black"
                    text
                    @click="readMore(article.web_url)"
                  >
                    Read more
                  </v-btn>
                </v-card-actions>
  
              </v-card>
            </v-col>
        </v-row>
          <v-row>
            <v-col>
                <div id="stranice">
        <button id="nazad" :disabled="page === 0" @click="previousPage">Previous</button>
        <span id="brojStr">Page {{ page + 1 }}</span>
        <button id="napred" :disabled="articles.length === 0" @click="nextPage">Next</button>
        </div>
            </v-col>
          </v-row>
        </v-container>
  </template>

  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        searchTerm: '',
        articles: [],
        page: 0
      };
    },
    methods: {
      async searchArticles() {
        try {
          this.page = 0; // Reset page when performing a new search
          await this.fetchArticles();
        } catch (error) {
          console.error(error);
        }
      },
      async previousPage() {
        if (this.page > 0) {
          this.page--;
          await this.fetchArticles();
        }
      },
      async nextPage() {
        this.page++;
        await this.fetchArticles();
      },
      async fetchArticles() {
        try {
          const response = await axios.get('https://api.nytimes.com/svc/search/v2/articlesearch.json', {
            params: {
              'api-key': '0EoubO7iGGZx3n4cvb2LyO6SnmNMssze',
              q: this.searchTerm,
              page: this.page
            }
          });
          this.articles = response.data.response.docs;
        } catch (error) {
          console.error(error);
        }
      },
            readMore(url) {
            window.open(url, '_blank');
        }
    },

    };

  </script>
  
<style>
#naslov {
    padding-left: 15px;
    padding-top: 15px;
    padding-right: 15px;
    padding-bottom: 15px;
}

#stranice {
    padding-left: 15px;
    padding-top: 15px;
    padding-right: 15px;
    text-align: center;
}

#brojStr {
    padding-left: 10px;
    padding-top: 10px;
    padding-right: 10px;
    padding-bottom: 10px;
    border-radius: 10px;
}

#napred {
    padding-left: 22px;
    padding-top: 10px;
    padding-right: 22px;
    padding-bottom: 10px;
    border-radius: 10px;
}

#nazad {
    padding-left: 10px;
    padding-top: 10px;
    padding-right: 10px;
    padding-bottom: 10px;
    border-radius: 10px;
}

#nazad:hover {
    box-shadow: 0 12px 16px 0 rgba(0,0,0,0.24),0 17px 50px 0 rgba(0,0,0,0.19);
}

#napred:hover {
    box-shadow: 0 12px 16px 0 rgba(0,0,0,0.24),0 17px 50px 0 rgba(0,0,0,0.19);
}

</style>
