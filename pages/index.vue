<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <v-container>
        <v-row>
          <v-col cols="12" md="12">
            <v-text-field
              v-model="zipcode"
              :counter="7"
              label="郵便番号（ハイフンなし）"
              outlined
              dense
              required
            ></v-text-field>
          </v-col>
        </v-row>
        <v-btn class="mr-4" @click="search">検索</v-btn>
      </v-container>
      <v-card>
        <v-card-title class="headline"></v-card-title>
        <v-card-text>
          <v-simple-table>
            <template v-slot:default>
              <thead>
                <tr>
                  <th class="text-left">住所</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="list in addressList" :key="list.address1">
                  <td>{{ list.address1 }}&nbsp;{{ list.address2 }}&nbsp;{{ list.address3 }}</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </v-card-text>
        <v-card-actions></v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import axios from '@nuxtjs/axios'
export default {
  components: {},
  data: function() {
    return {
      zipcode: '1040061',
      addressList: []
    }
  },
  methods: {
    async search() {
      await this.$axios
        .$get('/zipcode-api/api/search?zipcode=' + this.zipcode)
        .then((res) => {
          this.addressList = res.results
        })
        .catch((e) => {
          console.log(e)
        })
    }
  }
}
</script>
