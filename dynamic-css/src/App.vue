<template>
  <div id="main-app">
      <!-- 1) Start the Effect with the Button. The Effect should alternate the "highlight" or "shrink" class on each new setInterval tick (attach respective class to the div with id "effect" below) -->
  <div>
    <button @click="startEffect">Start Effect</button>
    <button @click="stopEffect">Stop Effect</button>
    <div id="effect" :class="effectClass"></div>
  </div>
  <hr>
  <!-- 2) Create a couple of CSS classes and attach them via the array syntax -->
  <div :class="['border--medium', 'bg-red']">I got no class :(</div>
  <!-- 3) Let the user enter a class (create some example classes) and attach it -->
  <hr>
  <div>
    <input type="text" v-model="customClass" placeholder="Set example of class eg bg--red">
    <div :class="customClass"></div>
  </div>
  <hr>
  <!-- 4) Let the user enter a class and enter true/ false for another class (create some example classes) and attach the classes -->
  <div>
    <input type="text" v-model="propertyName">
    <input type="text" v-model="propertyValue">
    <div class="box" :class="boxCustomClasses"></div>
  </div>
  <!-- 5) Repeat 3) but now with values for styles (instead of class names). Attach the respective styles.  -->
  <hr>
  <div>
    <input type="text" v-model="customStyles">
    <div :style="customStyles"></div>
  </div>
  <!-- 6) Create a simple progress bar with setInterval and style bindings. Start it by hitting the below button. -->
  <hr>
  <div>
    <button @click="startProgress">Start Progress</button>
    <button @click="resetProgress">Reset Progress</button>
    <div class="progress-bar"
         :style="{width: progesWidth + 'px'}"></div>
  </div>

  </div>
</template>

<script>
export default {
  name: 'main-app',
  data () {
    return {
      effectClass: 'shrink',
      customClass: 'box bg--red',
      effectInterval: null,
      progressInterval: null,
      active: true,
      dotted: true,
      propertyName: '',
      propertyValue: '',
      boxClasses: [],
      customStyles: '',
      progesWidth: 0
    }
  },

  computed: {
    boxCustomClasses() {
      if(this[this.propertyName] != undefined && this.propertyValue) {
        if(this.propertyValue == 'true') {
          this[this.propertyName] = true;
          this.boxClasses.push(this.propertyName);
        } else if(this.propertyValue == 'false') {
          const index = this.boxClasses.indexOf(this.propertyName);
          this[this.propertyName] = false;
          this.boxClasses.splice(index, 1);
        }
      }

      return this.boxClasses;
    }
  },

  methods: {
    startProgress() {
      const maxWidth = 400;
      const step = 20;
      const interval = 500;

      this.progressInterval = setInterval(() => {
        if(this.progesWidth < maxWidth) {
          this.progesWidth += step;
        } else {
          clearInterval(this.progressInterval);
        }
      }, interval);
    },

    resetProgress() {
      this.progesWidth = 0;
      clearInterval(this.progressInterval);
    },

    stopEffect() {
      clearInterval(this.effectInterval);
    },

    startEffect() {
      const interval = 1000;

      this.effectInterval = setInterval(() => {
        this.effectClass = this.effectClass == 'shrink' ? 'highlight' : 'shrink';
      }, interval);
    }
  }
}
</script>

<style>
#effect {
  width: 100px;
  height: 100px;
  border: 1px solid black;
}

.highlight {
  background-color: red;
  width: 200px !important;
}

.shrink {
  background-color: gray;
  width: 50px !important;
}

.progress-bar {
  height: 50px;
  background-color: red;
}

.border--medium {
  border: 1em solid #ccc;
}

.bg--red {
  background-color: red;
}

.box {
  width: 100px;
  height: 100px;
}

.active {
  border: 1px solid #efefef;
  background-color: green;
}

.dotted {
  border: 4px dotted red;
}
</style>
