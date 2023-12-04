<template>
  <div class="home">
    <img class="myPhoto" alt="Got Logo" src="../assets/home.webp" />
    <HelloWorld msg="Welcome to Game Of Thrones Page" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    HelloWorld,
  },
};
</script>

<style>
.myPhoto {
  display: block;
  margin: 2rem auto;
  width: 60%;

  border-radius: 50px;
  box-shadow: 0px 1px 6px 1px rgba(48, 16, 232, 0.75);
  -webkit-box-shadow: 0px 1px 7px 1px rgba(48, 16, 232, 0.75);
  -moz-box-shadow: 0px 1px 7px 1px rgba(48, 16, 232, 0.75);
}
img:hover {
  cursor: pointer;
}
</style>
