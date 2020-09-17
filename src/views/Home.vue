<template>
  <div class="home">
    <BookGrid />
  </div>
</template>

<script>
// @ is an alias to /src
import BookGrid from '@/components/BookGrid.vue'

export default {
  name: 'Home',
  components: {
    BookGrid
  }
}
</script>
