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
            v-if="articles.indexOf(article) >= (page - 1) * 9 && articles.indexOf(article) < page * 9"
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
              color="black"
         ></v-pagination>
          </v-col>
        </v-row>
        <v-dialog
        v-model="dialog"
        persistent
        max-width="600px"
        
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            color="black"
            dark
            v-bind="attrs"
            v-on="on"
            style="margin: 20px"
          >
            Add Article
          </v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span style="text-align: center;" class="text-h5">Add new Article</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col
                  cols="12"
                  sm="6"
                  md="4"
                >
                  <v-text-field
                    label="Headline*"
                    required
                    v-model="headline"
                  ></v-text-field>
                </v-col>
                <v-col
                  cols="12"
                  sm="6"
                >
                  <v-text-field
                    label="Writer*"
                    required
                    v-model="writer"
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field
                    label="Description*"
                    required
                    v-model="description"
                  ></v-text-field>
                </v-col>
                
                <v-col
                  cols="12"
                  sm="6"
                >
                <v-autocomplete
                    :items="sections"
                    label="Sections"
                    v-model="allSections"
                  ></v-autocomplete>
                </v-col>
              </v-row>
            </v-container>
            <small style="color: rgb(221, 20, 20);">*required field</small>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              color="black"
              text
              @click="dialog = false"
            >
              Close
            </v-btn>
            <v-btn
              color="black"
              text
              @click="addArticle()"
            >
              Save
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    <v-cols>
      <div v-if="alert" style=" margin: 15px; padding-top: 15px;">
        <v-alert type="success"
        v-model="alert"
        dismissible>
        Article added successfully!
    </v-alert>
    </div>
        </v-cols>
      </v-container>
</template>

<script>
  // import HelloWorld from '../components/HelloWorld'

  export default {
    name: 'Home',

    data() {
      return {
        test: 'Testna varijabla',
        articles: [],
        page: 1,
        search: '',
        dialog: false,
        alert: false,
        headline: '',
        writer: '',
        description: '',
        allSections: '',
        sections: [
        {value: 1, text: 'Bussiness'},
        {value: 2, text: 'Politics'},
        {value: 3, text: 'Sports'},
        {value: 4, text: 'Technology'},
        {value: 5, text: 'Science'},
        {value: 6, text: 'Health'},
        {value: 7, text: 'Arts'},
        {value: 8, text: 'Travel'},
        {value: 9, text: 'Food'},
        {value: 10, text: 'Style'},
        {value: 11, text: 'Magazine'},
        ]
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

      addArticle: function(){
        this.dialog = false
        this.alert = true
        
        if((this.headline == '') || (this.writer == '') || (this.description == '')){
          alert('You need to fill all of the required fields!')
          this.dialog = true
          this.alert = false
        } else {
          this.headline = ''
          this.writer = ''
          this.description = ''
          this.sections = ''
        }
      }

      

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