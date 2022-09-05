<template>
  <div id="app">
    <h1 title="YEEAH HELLOOOO00">Hello hello wroLD!!1</h1>
    <header>
      <h2>this is a sass python-like syntax test</h2>
      <button @click="boxAmount">Enter the amount of boxes to render</button>



      <div id="transD">
        <h3 v-if="!start">Select a box</h3>
        <h3 v-else>You selected box&nbsp;</h3>
        <Transition name="slide">
          <h3 v-if="render">{{ msg }}</h3>
        </Transition>

      </div>

    </header>

    <!-- <div v-for="i in amount" :key="i" class="flex-item" @click="test(i)" :ref="'box-' + i">
        {{ i }}
      </div> -->

    <div class="flex-container" v-if="safeMode">
      <div class="flex-item" v-for="(i, index) in amount" :key="i" @click="test(i)">
        <span v-if="index <= 99">
          {{ i }}</span>
      </div>
    </div>
    <div class="flex-container" :class="{ scrollLock: pop }" v-else>
      <span class="flex-item" v-for="i in amount" :key="i" @click="test(i)">
        {{ i }}</span>
    </div>

    <Transition name="fade">
      <div v-if="pop" id="popup-bg" @click="this.pop = false"></div>
    </Transition>
    <Transition name="appear">
      <div id="popup" tabindex="0" @keyup.esc="this.pop = false" @keyup.enter="this.pop = false" v-if="pop">
        <input :max="this.max" type="number" min="0" v-model="amount" ref="input" />
        <button title="Cap max box amount to 100, OFF sets the max amount to 100000, go over 1000 on your own risk"
          @click="toggleSafe">Safe Mode {{ safeStatus }}</button>
        <button @click="this.pop = false">OK</button>
      </div>
    </Transition>
  </div>
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
      max: 100,
      safeMode: true,
      safeStatus: 'ON'
    }
  },
  mounted() {
    // add a class scrolllock to the body when the popup is open
    this.$watch('pop', function (val) {
      if (val) {
        document.body.classList.add('scrollLock')
      } else {
        document.body.classList.remove('scrollLock')
      }
    })
  },
  methods: {
    boxAmount() {
      this.pop = true;
      //wait half a second
      setTimeout(() => {
        this.$refs.input.focus();
      }, 300);

    },
    toggleSafe() {
      this.safeMode = !this.safeMode;
      this.safeStatus = this.safeMode ? 'ON' : 'OFF';
      this.max = this.safeMode ? 100 : 100000;
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

*
  margin: 0
  padding: 0
  box-sizing: border-box

// html
//   overflow: hidden

.scrollLock
  overflow: hidden

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

.appear-enter-active, .appear-leave-active
  transition: all 0.2s ease

.appear-leave-to, .appear-enter-from
  opacity: 0
  transform: translateY(-50px)

header
  position: sticky
  top: 0
  background-color: white
  z-index: 2
  padding: 20px 0 20px 0
  display: flex
  flex-direction: column
  align-items: center
  justify-content: center
  gap: 20px

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
    z-index: 1

#popup-bg
  position: fixed
  top: 0
  left: 0
  right: 0
  bottom: 0
  min-height: 100vh
  min-width: 100%
  background-color: rgba(0, 0, 0, 0.5)
  z-index: 4
  margin: 0
  padding: 0
  backdrop-filter: blur(5px)

#popup
  position: fixed
  top: 0
  left: 0
  width: 100%
  height: calc(100vh - 169px)
  display: flex
  justify-content: center
  align-items: center
  z-index: 5
  gap: 20px
  flex-direction: column
  *
    width: 200px
    &:focus
    outline: none

  input
    padding: 10px 20px 10px 20px
    border: none
    border-radius: 5px
    font-size: 1.2em
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
  // &.scrollLock
    // overflow: hidden
    // height: calc( 100vh - 200px)
  .flex-item
    cursor: pointer
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
    &:empty
      display: none
    &:hover
      background-color: $secondary
      color: white
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
