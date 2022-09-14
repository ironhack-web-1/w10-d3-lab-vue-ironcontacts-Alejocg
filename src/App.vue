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
            <a class="nav-link" href="#buttons">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/">Refresh</a>
          </li>
          <li class="nav-item">
            <a @click="loadAllContacts()" class="nav-link" href="#buttons"
              >Load all contacts</a
            >
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <div>
    <div id="head" class="card">
      <div class="card-body">My IronContacts VIP agenda</div>
    </div>

    <div id="buttons">
      <button
        @click="addRandomContact(), randomNumber()"
        type="button"
        class="btn btn-primary"
        id="button1"
      >
        Add Random Contact
      </button>
      <button
        @click="sortByName()"
        id="button1"
        type="button"
        class="btn btn-success"
      >
        Sort By Name
      </button>
      <button
        @click="sortByPopularity()"
        id="button1"
        type="button"
        class="btn btn-warning"
      >
        Sort By Popularity
      </button>
      <button
        @click="removeAContact()"
        id="button1"
        type="button"
        class="btn btn-danger"
      >
        Remove a contact
      </button>
      <button
        @click="loadAllContacts()"
        id="button1"
        type="button"
        class="btn btn-info"
      >
        Load all contacts
      </button>
    </div>

    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">Picture</th>
          <th scope="col">Name</th>
          <th scope="col">Popularity</th>
          <th scope="col">Won Oscar</th>
          <th scope="col">Won Emy</th>
          <th scope="col">Phone</th>
          <th scope="col">Remove Contact</th>
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

        <td v-if="item.wonEmmy">🌟</td>
        <td v-else>⏳</td>
        <td id="pointer" @click="alertPhone(), randomNumber()">📞</td>
        <td id="pointer" @click="removeThisContact(index)">
          🗑️
        </td>
      </tr>
    </table>
  </div>
  <div class="other-options"><a href="/">↻ Refresh ↻ </a></div>
  <div class="other-options" id="pointer" @click="newMeContact()">🛑 Do not click 🛑</div>
</template>

<script>
import contacts from "./contacts.json";

export default {
  name: "App",

  data() {
    return {
      list: contacts,
      reducedList: [],
      newContact: [],
      random: 0,
      randomContact: 0,
      new: [
  {
    "name": "🌟 Alejo C 🌟",
    "pictureUrl": "https://i.pinimg.com/originals/af/55/09/af550933086c43868d53f01b745605dd.jpg",
    "popularity": 9000,
    "id": "11731992-0604-4bee-80d5-67ad845d0a38",
    "wonOscar": true,
    "wonEmmy": true
  },]

    };
  },

  methods: {
    print() {
      console.log(this.reducedList);
      console.log(this.random);
    },
    lessContacts() {
      this.reducedList = this.list.splice(this.random, 5);
    },
    randomNumber() {
      this.random = Math.floor(Math.random() * this.list.length) + 1;
      console.log(this.random);
    },
    addRandomContact() {
      this.reducedList.push(contacts[this.random]);
    },

    sortByName() {
      this.reducedList.sort((a, b) => a.name.localeCompare(b.name));
    },

    sortByPopularity() {
      this.reducedList.sort(function (a, b) {
        return parseFloat(b.popularity) - parseFloat(a.popularity);
      });
    },

    removeAContact() {
      this.reducedList.pop(contacts[this.random]);
    },
    removeThisContact(index) {
      this.reducedList.splice(index, 1)
    },
    loadAllContacts() {
      this.reducedList = this.list;
    },
    alertPhone() {
      alert("+" + this.random + this.random * 132456);
    },
    newMeContact(){
      this.reducedList.push(this.new[0]);
    }
  },
  mounted() {
    this.randomNumber();
    this.lessContacts();
    this.print();
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
  top: 0;
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
  width: 5em;
  height: 120px;
  overflow: hidden;
  align-items: center;
}

#buttons {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  align-content: center;
  justify-content: space-evenly;
  align-items: center;
  margin-top: 20px;
  margin-bottom: 20px;
}

button {
  display: flex;
  padding: 5px;
}

#pointer {
  cursor: pointer;
}

td {
  padding: 5px;
}

#row {
  border: 0px;
  padding-left: 0px;
}

#button1 {
  border: 5px;
  padding: 5px;
  color: white;
}

.other-options {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  align-content: center;
  justify-content: space-evenly;
  align-items: center;
  font-size: 30px;
  border: 20px;
}

.other-options a{
  color: black;
}

a:link {
  color: black;
  text-decoration: none;
} /* unvisited link */

</style>
