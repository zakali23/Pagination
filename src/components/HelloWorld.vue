<template>
  <div>
    <h1>{{title}}</h1>
    <ul>
      <li v-for="(item,i) in items" :key="i">{{item.age}}</li>
    </ul>
    <paginate
      :page-count="count"
      :page-range="3"
      :margin-pages="2"
      :click-handler="clickCallback"
      :prev-text="'<'"
      :next-text="'>'"
      :container-class="'pagination'"
      :page-class="'page-item'"
    ></paginate>
  </div>
</template>

<script>
import Paginate from "vuejs-paginate";
import users from "../Users.js";
export default {
  name: "HelloWorld",
  components: {
    Paginate
  },
  props: {
    msg: String
  },
  mounted() {
    return this.fetchUser();
  },
  data: function() {
    return {
      title: "Paginations",
      users,
      items: [],
      size: 4
    };
  },
  computed: {
    count() {
      return Math.ceil(users.length / this.size);
    }
  },
  methods: {
    clickCallback(pageNum) {
      let fin = pageNum * this.size;
      let debut = fin - this.size;
      return (this.items = users.slice(debut, fin));
    },
    fetchUser() {
      return (this.items = this.users.filter((user, i) => i < 4));
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
.pagination {
  display: flex;
}
.page-item {
  flex-direction: row;
}
</style>
