<template>
  <b-row>
    <b-col cols="12">
      <h2>
        Books List
        <b-link href="#/add-book">(Add Book)</b-link>
      </h2>
      <b-table striped hover :items="books" :fields="fields">
        <template slot="actions">
          <b-btn size="sm" @click.stop="details(row.item)">Details</b-btn>
        </template>
      </b-table>
    </b-col>
  </b-row>
</template>

<script>

import axios from 'axios'

export default {
  name: 'BookList',
  data () {
    return {
      fields: {
        isbn: { label: 'ISBN', sortable: true, 'class': 'text-center' },
        title: { label: 'Book Title', sortable: true },
        actions: { label: 'Action', 'class': 'text-center' }
      },
      books: []
    }
  },
  created () {
    axios.get(`http://localhost:3000/book`)
    .then(response => {
      this.books = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  },
  methods: {
    details (book) {
      this.$router.push({
        name: 'ShowBook',
        params: { id: book._id }
      })
    }
  }
}
</script>
