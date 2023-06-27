<template>
  <div class="about">  
    <v-row style="text-align: center;">
      <v-col>
        <h1>O projektu</h1>
        <br> <br>
        <p>
          Projekt napravljen u sklopu kolegija "Informatički projekt 2" koristeći Vue.js, Vuetify i
          <a href="https://developer.nytimes.com/apis" target="_blank" >NY Times API</a> za dohvaćanje podataka.
        </p>
        <p>
          Aplikacija omogućuje pregled najpopularnijih članaka u tome danu i pretraživanje članaka po ključnim riječima.
        </p>
        <p>
          Napravljena je u svrhe učenja i nije namijenjena za komercijalnu upotrebu.
        </p>
        <p>
          Izvorni kod se može pronaći na
          <a href=""
            >GitHub</a
          >.
        </p>
        <p>
          Made by: Oliver Vujica, Petar Kožul
        </p>
      </v-col>
    </v-row>

    <div v-if="alert" style=" margin: 15px; padding-top: 15px;">
      <v-alert type="success"
      v-model="alert"
      dismissible>
      Successfully subscribed
    </v-alert>
    </div>

    <h2 style="text-align: center; margin: 15px; padding-top: 15px;">Subscribe to New York Times to get the newest articles directly to the mail.</h2>
    <v-row justify="center">


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
            Subscribe
          </v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span class="text-h5">Subscription form</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col
                  cols="12"
                  sm="6"
                >
                  <v-text-field
                    label="First name*"
                    required
                    v-model="first_name"
                  ></v-text-field>
                </v-col>
                <v-col
                  cols="12"
                  sm="6"
                >
                  <v-text-field
                    label="Last name*"
                    required
                    v-model="last_name"
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field
                    label="Email*"
                    required
                    v-model="email"
                  ></v-text-field>
                </v-col>
                <v-col
                  cols="12"
                  sm="6"
                >
                  <v-text-field
                    
                    label="Age*"
                    required
                    v-model="age"
                  ></v-text-field>
                </v-col>
                <v-col
                  cols="12"
                  sm="6"
                >
                <v-autocomplete
                    :items="topics"
                    label="Your topics of interest*"
                    v-model="favourite_topics"
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
              @click="saveSub()"
            >
              Save
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>
  </div>
</template>


<script>
  export default {
    data: () => ({
      dialog: false,
      alert: false,
      first_name: '',
      last_name: '',
      email: '',
      age: '', 
      favourite_topics: '',
      topics: [
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
    }),
    methods: {
      saveSub: function(){
        this.dialog = false
        this.alert = true
        
        if((this.first_name == '') || (this.last_name == '') || (this.age == '') || (this.email == '')){
          alert('You need to fill all of the required fields!')
          this.dialog = true
          this.alert = false
        } else {
          this.first_name = ''
          this.last_name = ''
          this.age = ''
          this.email = ''
          this.favourite_topics = ''
        }
      }
    }
  }
</script>