<template class="row">
  <div class="hello col-4">
    <h1>{{ target.name }}</h1>
    <h1
      :class="{'text-success' : true, 'text-warning' : target.health < 75, 'text-danger' : target.health < 50}"
    >{{target.health}}</h1>
    <h1>{{target.hits}}</h1>
    <button class="btn btn-danger m-1" @click="punch();target.hits + 1">punch</button>
    <button
      class="btn btn-primary m-1"
      v-for="item in items"
      :key="item.name"
      @click="addItem(item)"
    >{{item.name}}</button>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: ["targetName"],
  data() {
    return {
      target: {
        name: this.name,
        health: 100,
        hits: 0,
        inventory: []
      },
      items: [
        {
          name: "block",
          mod: -0.5
        },
        {
          name: "charge",
          mod: 99
        }
      ]
    };
  },
  computed: {
    modTotal() {
      let total = 1;
      this.target.inventory.forEach(i => {
        total += i.mod;
      });
      return total;
    }
  },
  methods: {
    punch() {
      this.target.health -= 1 * this.modTotal;
      this.target.hits++;
      this.target.inventory = [];
    },
    addItem(item) {
      this.target.inventory.push(item);
    },
    checkHealth() {
      let cl = "text-success";
      if (this.target.health < 50) {
        cl = "text-danger";
      } else if (this.target.health < 80) {
        cl = "text-warning";
      }
      return cl;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
img {
  height:345px; 
  margin-left: -200px;
}
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
a {
  color: #42b983;
}
</style>
