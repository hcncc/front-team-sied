<template>
  <div class="cards">
    <div class="card" v-for="post in posts" :key="post.id">
      <h6>{{ post.title }}</h6>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Post',
  data() {
    return {
      posts: []
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch("http://localhost:3333/post");
        if (!response.ok) {
          throw new Error("Erro na requisição");
        }
        const data = await response.json();
        this.posts = data;
        console.warn("os dados no array: ", this.posts);
      } catch (error) {
        console.error("Erro na requisição: ", error);
      }
    }
  }
}
</script>

<style scoped>
.cards {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-template-rows: auto;
  gap: 2px;
  height: 1000px;
  width: 1000px;
  background-color: white;
  color: black;
  padding: 10px;
}
.card {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  width: 200px;
  height: 50px;
  text-align: center;
  border: 1px solid #000;
  border-radius: 8px;
  box-shadow: 0px 2px 5px;
}
h6 {
  font-size: 25px;
}
</style>
