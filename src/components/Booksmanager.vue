<script setup>
  import { createBook, getBooks } from "../api/books";
</script>
<script>
  export default {
    name: "BooksManager",
    data() {
      return {
        books: [],
        newBook: {
          title: "",
          author: "",
          year: 2000,
        },
      };
    },
    mounted() {
      this.loadBooks();
    },
    methods: {
      async loadBooks() {
        this.books = await getBooks();
      },
      async addBook(book) {
        await createBook(book);
        await this.loadBooks();
      },
      async submitCreateBook() {
        await this.addBook(this.newBook);
      },
    },
  };
</script>
<template>
  <main class="">
    <h1 class="">Könyv kezelő rendszer</h1>

    <form
      @submit.prevent="submitCreateBook"
      class="border-2 border-gray-200 p-2 m-2 flex flex-col gap-4"
    >
      <div class="flex flex-col">
        <label for="title" class="">cím: </label>
        <input
          v-model="newBook.title"
          type="text"
          name="title"
          id=""
          class="border-2 border-gray-200 p-1"
        />

        <label for="author" class="">szerző: </label>
        <input
          v-model="newBook.author"
          type="text"
          name="author"
          id=""
          class="border-2 border-gray-200 p-1"
        />

        <label for="year" class="">év: </label>
        <input
          v-model="newBook.year"
          type="number"
          name="year"
          id=""
          class="border-2 border-gray-200 p-1"
        />
      </div>

      <button type="submit" class="border-2 border-gray-200 p-2">
        Létrehozás
      </button>
    </form>

    <table class="">
      <thead class="">
        <tr class="">
          <th class="">azonosító</th>
          <th class="">Cím</th>
          <th class="">szerző</th>
          <th class="">év</th>
          <th class="">művelet</th>
        </tr>
      </thead>
      <tbody class="">
        <tr v-for="book in books" :key="book.id" class="">
          <td class="">{{ book.id }}</td>
          <td class="">{{ book.title }}</td>
          <td class="">{{ book.author }}</td>
          <td class="">{{ book.year }}</td>
          <td class="">--</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
