<template>
  <v-container>
    <r-row>
        <r-col>
          <h2 id="naslov">Top Stories</h2>
           <br>
        </r-col>
      </r-row>
        <v-row>
          <v-col
            v-for="article in articles"
            v-if="articles.indexOf(article) >= (page - 1) * 10 && articles.indexOf(article) < page * 10"
            :key="article.title"
            cols="12" sm="6" md="4"
          >
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
                {{ article.byline }}
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
          </v-col>
        </v-row>

        <v-row>
          <v-col cols="12"> 
            <v-pagination
              v-model="page"
              :length="3"
         ></v-pagination>
          </v-col>
        </v-row>
        <v-dialog
      v-model="addArticle"
      width="500"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="black"
          dark
          v-bind="attrs"
          v-on="on"
        >
          Add Article
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          Add new article
        </v-card-title>

        <v-card-text>
          <new-form></new-form>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="addDialog = false; successAlert = true"
          >
            Submit
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-cols>
          <v-alert type="success" dismissible v-model="successAlert">
            Article added successfully!
          </v-alert>
        </v-cols>
      </v-container>
</template>

<script>
  // import HelloWorld from '../components/HelloWorld'
  import NewForm from '../components/NewForm'

  export default {
    name: 'Home',

    components: {
      NewForm,
    },

    data() {
      return {
        test: 'Testna varijabla',
        articles: [],
        page: 1,
        search: '',
        addDialog: false,
        successAlert: false,
      }
    },

    created() {
      this.getArticles();
    },
    methods: {
      getArticles() {
        let api = 'https://api.nytimes.com/svc/topstories/v2/home.json'
        this.axios.get(api, {
          params: {
            'api-key': '0EoubO7iGGZx3n4cvb2LyO6SnmNMssze',
          }
        }).then((response) => {
            console.log(response.data)
            this.articles = response.data.results
          })
      },      
  
      toURL(url) {
        window.open(url, '_blank')
      },

      //fetchEntriesDebounced() {
       // this._searchTimerId = setTimeout( () => {
        //  this.getArticles()
       // }, 500)
     // },
    },

    //components: {
    //  HelloWorld,
    //},
  }
</script>

<style>
#naslov {
  text-align: center;
}
</style>