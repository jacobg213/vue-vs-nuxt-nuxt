<template>
  <div class="about" itemscope="" itemtype="https://schema.org/Book">
    <h1>This is an about page</h1>
    <h3 itemprop="name" v-if="book.Title">Book: {{ book.Title }}</h3>
    <span style="display: block;" v-if="book.Subtitle">{{ book.Subtitle }}</span>
    <span itemprop="isbn" style="display: block;" v-if="book.ISBN">{{ book.ISBN }}</span>
    <p v-if="book.Description">{{ book.Description }}</p>
    <img itemprop="image" v-if="book.CoverThumb" :src="book.CoverThumb">
    <h4>Authors:</h4>
    <ul>
      <li itemprop="author" v-for="author in book.Authors" :key="author.Name">{{ author.Name }}</li>
    </ul>
    <h4>Subjects:</h4>
    <ul>
      <li itemprop="genre" v-for="subject in book.Subjects" :key="subject">{{ subject }}</li>
    </ul>
  </div>
</template>

<script>
  import { mapState } from 'vuex';

  export default {
    computed: {
      ...mapState(['book']),
    },
    async fetch({ store }) {
      await store.dispatch('getBook');
    },
  };
</script>
