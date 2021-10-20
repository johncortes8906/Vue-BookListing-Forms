<template>
  <form
    v-on:submit.prevent="bookSubmit()"
    class=""
    action="#"
    method="post"
  >
    <input
      v-model="bookData.bookTitle"
      type="text"
      name="title"
      value=""
      placeholder="Book Title"
    />
    <input
      v-model="bookData.bookAuthor"
      type="text"
      name="author"
      value=""
      placeholder="Book Author"
    />
    <div>
      <input
        type="checkbox"
        id="finishedReading"
        v-model="bookData.finishedReading"
      />
      <label for="finishedReading">Finished reading?</label>
    </div>
    <div>
      <input v-model="bookData.ownership" type="radio" id="borrowed" name="ownership" value="borrowed" />  
      <label for="borrowed">Borrowed</label>
      <input v-model="bookData.ownership" type="radio" id="borrowed" name="ownership" value="bought" />  
      <label for="bought">Bought</label>
    </div>
    <button type="submit" name="button">Add Book</button>
  </form>
</template>

<script>
export default {
  name: "BookForm",
  props: ["books"],
  data() {
    return {
      bookData: {
        bookTitle: "",
        bookAuthor: "",
        finishedReading: false,
        ownership: [],
      },
    };
  },
  methods: {
    bookSubmit(bookTitle, bookAuthor) {
      this.$emit("addBook", bookTitle, bookAuthor);
    },
  },
};
</script>

<style>
</style>
