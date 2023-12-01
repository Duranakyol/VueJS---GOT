<template>
  <div class="persons">
    <h1>PERSONS</h1>
    <input
      type="search"
      id="site-search"
      name="q"
      placeholder="Schreib hier..."
    />
    <button class="searchButton">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="18"
        height="18"
        fill="currentColor"
        class="bi bi-search"
        viewBox="0 0 16 16"
      >
        <path
          d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0"
        />
      </svg>
      SEARCH
    </button>
    <div class="list">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">Name</th>
            <th scope="col">Slug</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(person, index) in persons" :key="person.id">
            <td>{{ person.name }}</td>
            <td>{{ person.slug }}</td>
            <button @click="showQuotes(index)">Quotes</button>
            <button class="myShow" @click="showHouses(index)">Houses</button>
          </tr>
        </tbody>
      </table>

      <div class="details" v-if="selectedPerson !== null">
        <h3>Quotes of {{ persons[selectedPerson].name }}</h3>
        <ul>
          <li
            v-for="(quote, index) in persons[selectedPerson].quotes"
            :key="index"
          >
            {{ quote }}
          </li>
        </ul>
      </div>

      <div class="details" v-if="selectedPerson2 !== null">
        <h3>Houses of {{ persons[selectedPerson2].name }} - Slug & Name</h3>
        <ul>
          <li v-for="house in persons[selectedPerson2].house" :key="house">
            {{ house }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      persons: null,
      selectedPerson: null,
      selectedPerson2: null,
    };
  },
  methods: {
    showQuotes(index) {
      this.selectedPerson = index;
    },
    showHouses(index) {
      this.selectedPerson2 = index;
    },
  },
  created: function () {
    axios
      .get("https://api.gameofthronesquotes.xyz/v1/characters")
      .then((res) => {
        this.persons = res.data;
      });
  },
};
</script>

<style>
h1 {
  color: red;
  font-weight: bold;
}
input {
  width: 16rem;
  height: 2rem;
}
.searchButton {
  margin: 2px;
  cursor: pointer;
  background-color: blueviolet;
  border: none;
  color: white;
  padding: 4px 6px;
}
.list {
  margin: 20px;
}
.details {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 2rem auto;
  width: 80%;
  height: 500px;
  background-image: url("../assets/persons.jpg");
  background-size: 100%;
  background-repeat: no;
  color: white;
  border-radius: 20px;
}

h3 {
  font-weight: bold;
}

.myShow {
  margin-left: 10px;
}

ul li {
  list-style: none;
}
</style>
