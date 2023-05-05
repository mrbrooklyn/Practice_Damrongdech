<template>
  <div>
    <p v-for="manu in manufacturer" :key="manu.id">
      {{ manu.id }} - {{ manu.Title }}
    </p>
    <input placeholder="id" v-model="id" />
    <input placeholder="Title" v-model="Title" />
    <button @click="post()">Post</button>
    <button @click="put()">Put</button>
    <button @click="remove()">Delete</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      text: "test",
      manufacturer: [{ id: 1, Title: "test1" }],
      id: "",
      Title: "",
    };
  },
  created() {
    this.get();
  },
  methods: {
    get() {
      axios.get("https://localhost:7127/api/manufacturers").then((respone) => {
        this.manufacturer = respone.data;
      });
    },
    post() {
      axios
        .post("https://localhost:7127/api/manufacturers", {
          id: this.id,
          Title: this.Title,
        })
        .then((respone) => {
          this.get();
        });
    },
    remove() {
      axios
        .delete("https://localhost:7127/api/manufacturers/" + this.id)
        .then((respone) => {
          this.get();
        });
    },
    put() {
      axios
        .put("https://localhost:7127/api/manufacturers/" + this.id, {
          id: this.id,
          Title: this.Title,
        })
        .then((respone) => {
          this.get();
        });
    },
  },
};
</script>