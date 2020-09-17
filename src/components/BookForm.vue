<template>
  <div>
    <h2>{{ act }} a Book</h2>
    <form>
      <fieldset>
        <legend>{{ act }} a Book</legend>
<!--
        <div class="field" v-for="(item, key, i) in book" :key="key">
          <label class="label" :for="key">{{ key }}:</label>
          <input type="text" v-model="item.value" required="" />
          {{ i }} - {{ item }}
        </div>
-->
        <div class="field">
          <label class="label" for="Name">Name:</label>
          <input type="text" v-model="book.Name.value" required="" />
        </div>
        <div class="field">
          <label class="label" for="Author">Author:</label>
          <input type="text" v-model="book.Author.value" required="" />
        </div>
        <div class="field">
          <label class="label" for="ISBN">ISBN:</label>
          <input type="text" v-model="book.ISBN.value" required="" />
        </div>
        <div class="field">
          <label class="label" for="Genre">Genre:</label>
          <input type="text" v-model="book.Genre.value" required="" />
        </div>
        <div>
          <button @click="submit" type="submit">Save</button>
          <button @click="cancel">Cancel</button>
        </div>
      </fieldset>
    </form>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import router from '../router'
const INIT = (key) => {
  return {
    value: ''
  }
}

export default {
  name: 'BooKForm',
  props: ['act', 'id'],
  data () {
    return {
      state: 'Add',
      book: {
        Name: INIT('Name'),
        Author: INIT('Author'),
        ISBN: INIT('ISBN'),
        Genre: INIT('Genre')
      },
      keys: []
    }
  },
  methods: {
    ...mapActions(['createNew', 'updateOne']),
    submit () {
      const book = {}
      const keys = Object.keys(this.book)
      keys.forEach(key => (book[key] = this.book[key].value))
      if (this.act === 'add') {
        this.createNew(book)
      } else {
        book.ID = this.id
        this.updateOne(book)
      }
      router.push('/')
    },
    cancel () {
      router.push('/')
    }
  },
  computed: mapGetters(['theBook']),
  beforeCreated () {
    this.keys = Object.keys(this.book)
  },
  created () {
    console.log('#form:', this.act, '/', this.id)
    if (this.act === 'update') {
      const aBook = this.theBook(this.id)
      if (aBook) {
        this.book.Name.value = aBook.Name
        this.book.Author.value = aBook.Author
        this.book.ISBN.value = aBook.ISBN
        this.book.Genre.value = aBook.Genre
      }
    }
  }
}
</script>

<style scoped>
form {
  width: 600px;
  text-align: center;
  display: inline-block;
}
legend {
  font-size: 24px;
  padding: 10px;
}
div.field {
  padding: 15px;
}
label.label {
  display: inline-block;
  width: 80px;
  position: relative;
}
input {
  width: 250px;
  box-sizing: border-box;
}
button {
  margin: 10px;
  cursor: pointer;
}
</style>
