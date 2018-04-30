<template>
  <div class="hello">
    <h2>Essential Links</h2>
    <div class="posts" v-for="post in posts" v-bind:key="post.id">
      <h3>{{ post.title }}</h3>
      <p>{{ post.text }}</p>
    </div>
  </div>
</template>

<script>
import db from "./firebaseInit";
export default {
  name: "HelloWorld",
  data() {
    return {
      posts: [],
      loading: true
    };
  },
  created() {
    db
      .collection("posts")
      .get()
      .then(querySnapshot => {
        querySnapshot.forEach(doc => {
          const data = {
            id: doc.id,
            title: doc.data().title,
            text: doc.data().text,
            date: doc.data().date
          };
          this.posts.push(data);
        });
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
