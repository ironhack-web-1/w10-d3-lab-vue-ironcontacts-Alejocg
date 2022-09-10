<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
      <a class="navbar-brand" href="">Ironcontacts</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarTogglerDemo02"
        aria-controls="navbarTogglerDemo02"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarTogglerDemo02">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item">
            <a class="nav-link" href="/">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/">Contacts</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <div>
    <div id="head" class="card">
      <div class="card-body">My IronContacts VIP agenda</div>
    </div>

    <div id=buttons>
      <button type="button" class="btn btn-primary">Add Random Contact</button>
      <button type="button" class="btn btn-success">Sort By Name</button>
      <button type="button" class="btn btn-warning">Sort By Popularity</button>
      <button type="button" class="btn btn-danger">Remove a contact</button>
    </div>

    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">Picture</th>
          <th scope="col">Name</th>
          <th scope="col">Popularity</th>
          <th scope="col">Won Oscar</th>
          <th scope="col">Won Emy</th>
        </tr>
      </thead>
      <tr
        class="img-thumbnail"
        id="list"
        v-for="(item, index) in reducedList"
        :key="index"
      >
        <div id="imgContainer">
          <td id="row" scope="row">
            <img :src="item.pictureUrl" :alt="item.name" />
          </td>
        </div>
        <td>{{ item.name }}</td>
        <td>{{ item.popularity.toFixed([2]) }}</td>
        <td v-if="item.wonOscar">🏆</td>
        <td v-else>⏳</td>

        <td v-if="item.wonEmmy">🏆</td>
        <td v-else>⏳</td>
      </tr>
    </table>
  </div>
</template>

<script>
import contacts from "./contacts.json";

export default {
  name: "App",

  data() {
    return {
      list: contacts,
      reducedList: "",
    };
  },

  methods: {
    print() {
      console.log(this.reducedList);
    },
    lessContacts() {
      this.reducedList = this.list.splice(0, 10);
    },
  },
  mounted() {
    this.print();
    this.lessContacts();
  },
};
</script>

<style scoped>
* {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
    "Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#app {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
}

nav {
  position: fixed;
  top:0;
  width: 100%;
}

#head {
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  align-content: center;
  justify-content: center;
  align-items: center;
  font-size: 35px;
}

table {
  background-color: aliceblue;
  align-items: normal;
  text-align: center;
}

#imgContainer {
  width: 140px;
  height: 140px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}

#imgContainer img {
  display: flex;
  justify-content: center;
  width: 100%;
  height: 120px;
  overflow: hidden;

  align-items: center;
}

#buttons {

  display: flex;
  flex-direction: row;
  align-content: center;
  justify-content: space-evenly;
  align-items: center;
  margin-top: 20px;
  margin-bottom: 20px;
}

button {
  display:flex;
}
</style>
