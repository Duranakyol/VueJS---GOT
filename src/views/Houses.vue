<template>
  <div class="houses">
    <h1>HOUSES</h1>
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
            <th scope="col">Slug</th>
            <th scope="col">Name</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(house, index) in houses" :key="house.id">
            <td>{{ house.slug }}</td>
            <td>{{ house.name }}</td>
            <button @click="showMembers(index)">Members</button>
          </tr>
        </tbody>
      </table>

      <div class="members" v-if="selectedHouse !== null">
        <h3>Members of {{ houses[selectedHouse].name }}</h3>
        <ul>
          <li
            v-for="(member, index) in houses[selectedHouse].members"
            :key="index"
          >
            {{ member.name }}
          </li>
        </ul>
        <h3>Members of {{ houses[selectedHouse].slug }}</h3>
        <ul>
          <li
            v-for="(member, index) in houses[selectedHouse].members"
            :key="index"
          >
            {{ member.slug }}
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
      houses: null,
      selectedHouse: null,
    };
  },
  methods: {
    showMembers(index) {
      this.selectedHouse = index;
    },
  },
  created: function () {
    axios.get("https://api.gameofthronesquotes.xyz/v1/houses").then((res) => {
      this.houses = res.data;
    });
  },
};
</script>

<style>
h1 {
  color: red;
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

.members {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 2rem auto;
  width: 80%;
  height: 500px;
  background-image: url("../assets/houses.jpeg");
  background-size: 100%;
  background-repeat: no;
  color: white;
  border-radius: 20px;
}

h3 {
  font-weight: bold;
}

ul li {
  list-style: none;
}
</style>
