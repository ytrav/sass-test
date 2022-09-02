<template>
  <h1 title="YEEAH HELLOOOO00">Hello hello wroLD!!1</h1>
  <header>
    <h2>this is a sass python-like syntax test</h2>
    <button @click="boxAmount">Enter the amount of boxes to render</button>
    <Transition name="fade">
      <div id="popup" v-if="pop">
        <input type="number" v-model="amount" ref="input" />
        <button @click="this.pop = false">OK</button>
      </div>
    </Transition>
    <Transition name="fade">
      <div v-if="pop" id="popup-bg" @click="this.pop = false"></div>
    </Transition>

    <div id="transD">
      <h3 v-if="!start">Select a box</h3>
      <h3 v-else>You selected box&nbsp;</h3>
      <Transition name="slide">
        <h3 v-if="render">{{ msg }}</h3>
      </Transition>
    </div>
  </header>
  <div class="flex-container">
    <div v-for="i in amount" :key="i" class="flex-item" @click="test(i)" :ref="'box-' + i">
      {{ i }}
    </div>
  </div>
  <!-- <button @click="isSelected = true">Click me</button> -->
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      msg: '',
      render: true,
      start: false,
      pop: false,
      amount: 0,
      isSelected: {
        n1: false,
        n2: false,
        n3: false,
        n4: false,
        n5: false,
      },
    }
  },
  methods: {
    boxAmount() {
      this.pop = true;
      //wait half a second
      setTimeout(() => {
      this.$refs.input.focus();
      }, 300);
    },
    test(i) {
      this.start = true;
      this.render = false;
      this.msg = i;
      setTimeout(() => {
        this.render = true;
      }, 200);
      this.$refs['box-' + i]
    },
  }
}
</script>

<style lang="sass">
$primary: rgb(30, 100, 15)
$secondary: rgb(30, 50, 15)

.fade-enter-active, .fade-leave-active
  transition: opacity .2s

.fade-leave-to, .fade-enter-from
  opacity: 0

.slide-enter-active, .slide-leave-active
  transition: transform 0.2s ease

.slide-leave-to
  transform: translateY(40px)

.slide-enter-from
  transform: translateY(-40px)

header
  position: sticky
  top: 0
  background-color: white
  z-index: 1
  padding: 20px 0 20px 0

button
  background-color: $primary
  color: white
  border: none
  padding: 10px 20px 10px 20px
  border-radius: 5px
  font-size: 1.2em
  cursor: pointer
  transition: background-color 0.1s ease-out
  &:hover
    background-color: $secondary

#popup-bg
  position: absolute
  top: 0
  left: 0
  right: 0
  bottom: 0
  background-color: rgba(0, 0, 0, 0.5)
  display: flex
  justify-content: center
  align-items: center
  z-index: 2
  margin: 0
  padding: 0

#popup
  position: absolute
  top: 0
  left: 0
  width: 100%
  height: calc(100vh - 169px)
  display: flex
  justify-content: center
  align-items: center
  z-index: 3
  input
    padding: 10px 20px 10px 20px
    border: none
    border-radius: 5px
    font-size: 1.2em
    margin-right: 20px
  button
    background-color: $primary
    color: white
    border: none
    padding: 10px 20px 10px 20px
    border-radius: 5px
    font-size: 1.2em
    cursor: pointer
    transition: background-color 0.1s ease-out
    &:hover
      background-color: $secondary


#transD
  height: 60px
  display: flex
  justify-content: center
  align-items: center
  overflow: hidden
h1
  color: $primary

h2
  color: $secondary
h1,h2, h3, div
  text-align: center
  font-family: sans-serif
  &:hover
    color: $secondary

.flex-container
  display: flex
  flex-wrap: wrap
  justify-content: center
  align-items: center
  align-content: center
  overflow: auto
  .selected
      background-color: $secondary !important
      transform: scale(0.9)
  .flex-item
    width: 100px
    height: 100px
    background-color: $primary
    margin: 10px
    display: flex
    justify-content: center
    align-items: center
    font-size: 2em
    color: white
    border-radius: 5px
    transition: transform 0.1s ease-out
    
    &:hover
      background-color: $secondary
      transform: scale(0.9)
</style>

<!-- <style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style> -->
