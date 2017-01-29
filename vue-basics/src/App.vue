<template>
  <div id="main-app">
    <h3>Basics</h3>

    <h2 v-once>{{ msg }}</h2>
    <div class="dir-ex">
      <a :href="link">Go to google</a>
    </div>
    <div class="say">{{ sayHello() }}</div>
    <hr>
    <p v-html="newsLink"></p

    <hr>
    <h3> Practice I</h3>

    <p>My name: {{ name }} ({{ age }})</p>
    <p>Multiply age: {{ age * 3 }}</p>
    <p>Random number: {{ generateRandom() }}</p>
    <img :src="meme" />
    <hr>
    <input :value="name" @input="updateName" type="text">
    <hr>
    <button @click="increase(2)">Click me</button>
    <p><strong>{{ counter }}</strong>
    <hr>
    <p @mousemove="updateCoordinates">
      Coordinates: {{ x }} / {{ y }}
      - <span @mousemove.stop.prevent="">DEAD SPOT</span>
    </p>

    <hr>
    <h3> Practice II</h3>
    <button @click="showAlert">Show alert</button>

    <p>
      <label for="value">Value:</label>
      <input type="text" id="value" @keydown="recordValue">
      <div>
        <strong>You type: {{ value }}</strong>
      </div>
    </p>

    <p>
      <label for="value">Value:</label>
      <input type="text" id="value" @keydown.13="recordValue">
      <div>
        <strong>You type: {{ value }}</strong>
      </div>
    </p>

    <h3>Computed properties</h3>

    <button @click="counter++">Increment</button>
    <button @click="secondCounter++">Second Increment</button>

    <p>Counter: {{ counter }}, secondCounter: {{ secondCounter }}</p>
    <p>Current Result: {{ currentResultMethod() }} | {{ currentResult }}</p>

    <hr>
    <h3> Practice III</h3>

    <button @click="value+=5">Add 5</button>
    <button @click="value++">Add 1</button>

    <p>Current value {{ value }}</p>
    <p>Current result: {{ result }}


  </div>
</template>

<script>
export default {
  name: 'main-app',

  data () {
    return {
      msg: 'Welcome to Your Vue.js App!!',
      link: 'http://google.com',
      newsLink: '<a href="http://wp.pl">WP news</a>',
      age: 30,
      name: 'Stefan',
      meme: 'https://static01.nyt.com/images/2016/08/05/us/05onfire1_xp/05onfire1_xp-master768-v2.jpg',
      counter: 0,
      secondCounter: 0,
      x: 0,
      y: 0,
      value: 0
    }
  },

  computed: {
    currentResult() {
      console.log('currentResult - computed');
      return this.counter > 5 ? 'Grater than 5' : 'Smaller than 5';
    },

    result() {
      return this.value > 37 ? 'it is bigger that 37' : 'sorry, we are not there';
    }
  },

  watch: {
    counter(value) {
      setTimeout(() => { this.counter = 0; }, 2000);
    },

    value(val) {
      setTimeout(() => { this.value = 0; }, 5000);
    }
  },

  methods: {
    currentResultMethod() {
      console.log('currentResult - method');
      return this.counter > 5 ? 'Grater than 5' : 'Smaller than 5';
    },

    showAlert() {
      alert('Hello');
    },

    recordValue(event) {
      this.value = event.target.value;
    },

    sayHello() {
      const newMsg = 'Hello World'
      this.msg = newMsg;
      return newMsg;
    },

    updateName(event) {
      this.name = event.target.value;
    },

    generateRandom() {
      return Math.random();
    },

    increase(step = 1) {
      this.counter += step;
    },

    updateCoordinates(event) {
      this.x = event.clientX;
      this.y = event.clientY;
    }
  }
}
</script>

<style>
#main-app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
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
