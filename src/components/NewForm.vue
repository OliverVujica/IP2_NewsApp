<template>
    <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col
          cols="12"
        >
          <v-text-field
            v-model="headline"
            :counter="10"
            label="Headline"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"
        >
          <v-text-field
            v-model="author"
            :counter="10"
            label="Author"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="20"
        >
          <v-text-field
            v-model="description"
            label="Description"
            required
          ></v-text-field>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
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