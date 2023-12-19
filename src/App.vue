<template>
<div class="container">
  <h1 v-text="name"></h1>
  <div class="inner-cursor" :style="{ top: cursorY + 'px', left: cursorX + 'px' }"></div>

  <h2>{{ name }} {{ verb }} {{ sentence }} {{ age }}</h2>

  <button @click="age++"> increase age</button>

  <button @click="age--"> decrease age</button>

  <div @click="changeName()" class="v">Click here to change name</div>

  <button @click="changeSentence('living his life at')">change sentence</button>

  <div v-if="bool">
    {{ name }}
  </div>
  <div v-else>
    This will only change when true:::::::::
  </div>

  <div v-show="bool">
    {{ age }}
  </div>

  <button @mouseover="changeState()">change state</button>
</div>

</template>

<script>

export default {
  data(){
    return{
      name: "Brandon",
      verb: "is",
      sentence: "living his best life at",
      age: 20,
      bool: true,
      cursorX: 0,
      cursorY: 0
    }
  },
  mounted() {
    // Add event listeners for mouse movement
    document.addEventListener("mousemove", this.updateCursorPosition);
  },
  before() {
    // Remove event listeners when component is destroyed
    document.removeEventListener("mousemove", this.updateCursorPosition);
  },
   methods : {
    
    changeName(){
      this.name = "Edward"
    },
    changeSentence(sentence){
      this.sentence = sentence
    },
     changeState(){
      this.bool = !this.bool
     },
     updateCursorPosition(event) {
      this.cursorX = event.clientX;
      this.cursorY = event.clientY;
    },
     
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.v{
  border: 1px solid black;
  cursor: none;
}
.container, button{
  cursor: none;
}

.inner-cursor {
  position: fixed;
  width: 13px;
  height: 13px;
  border-radius: 50%;
  background-color: #00f3b6;
  z-index: 5000;
  transform: translate(-50%, -50%);
  mix-blend-mode: difference;
  pointer-events: none;
  box-shadow: 1px 1px 7px 1px black;
  transition: width 0.5s, height 0.5s ease-in-out !important;
}

/* .inner-cursor.grow {
    width: 25px;
    height: 25px;
    transition: width .5s,height .5s ease-in-out!important
}

.outer-cursor {
    position: fixed;
    left: 10px;
    width: 25px;
    height: 25px;
    border: 1px solid #000000;
    border-radius: 50%;
    mix-blend-mode: difference;
    transform: translate(-50%,-50%);
    pointer-events: none;
    z-index: 5000;
    transition: none!important
} */
</style>
