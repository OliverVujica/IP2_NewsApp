<template>
    <v-dialog
        v-model="dialog"
        persistent
        max-width="600px" 
      >
        <template v-slot:activator="{ on, attrs }">
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
</template>

<script>
export default {
  data () {
    return {
    headline: '',
    author: '',
    description: '',
        }
    }
}
</script>