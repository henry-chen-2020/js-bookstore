<template>
  <div class="book">
    <BookForm :act="act" :id="id" />
  </div>
</template>

<script>
import BookForm from '../components/BookForm'
export default {
  props: ['act', 'id'],
  components: {
    BookForm
  }
}
</script>
