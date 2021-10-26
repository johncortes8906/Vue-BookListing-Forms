<template>
  <div>
    <h1>{{ title }}</h1>
    <ul>
      <h2>Filtered Books By Ownership</h2>
      <hr/>
      <select v-model="holding">
        <option v-for="filter in filters" :key="filter">{{ filter }}</option>
      </select>
      <hr/>
      <book-item v-for="book in filteredBooks" :key="book.id" :book="book"></book-item>
    </ul>
    <br />
    <hr />
    <book-form @addBook="appendBook"></book-form>
  </div>
</template>

<script>
import _ from "lodash";
import BookItem from "./BookItem";
import BookForm from "./BookForm";

export default {
  name: "BookList",
  data() {
    return {
      title: "All Books",
      states: ["Want to Read", "Read", "Reading"],
      filters: ["bought", "borrowed"],
      holding: "bought",
      books: [
        {
          title: "Self-Reliance",
          author: "Ralph Waldo Emerson",
          finishedReading: true,
          ownership: "borrowed",
        },
        {
          title: "American Gods",
          author: "Neil Gaiman",
          finishedReading: true,
          ownership: "bought",
        },
        {
          title: "Amusing Ourselves to Death",
          author: "Neil Postman",
          finishedReading: false,
          ownership: "borrowed",
        },
      ],
    };
  },
  components: {
    BookItem,
    BookForm,
  },
  computed: {
    filteredBooks() {
      return _.filter(this.books, ["ownership", this.holding]);
    },
  },
  methods: {
    appendBook(bookData) {
      this.books.push({
        title: bookData.bookTitle,
        author: bookData.bookAuthor,
        finishedReading: bookData.finishedReading,
        ownership: bookData.ownership,
      });
    },
  },
};
</script>

<style>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: block;
  margin: 0 10px;
}
</style>
