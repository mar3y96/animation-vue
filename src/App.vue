<template>
  <div class="container">
    <div class="block" :class="{ 'animate-left': animateLeft, 'animate-right': animateRight }"></div>
    <button @click="startAnimation">Animate</button>
  </div>
  <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>

  <div class="container">
    <transition name="para">
      <p v-if="visablPara">this is paragraph .....</p>
    </transition>
    <button @click="showPara">{{ visablPara?'hide para': ' Show para' }}</button>
  </div>
  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div>
</template>  

<script>
export default {
  data() {
    return {
      visablPara: false,
      dialogIsVisible: false,
      animateRight: false,
      animateLeft: false,
      foo: 'foooo'
    };
  },
  methods: {
    showDialog() {
      this.dialogIsVisible = true;
    },
    showPara() {
      this.visablPara = !this.visablPara;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    startAnimation() {
      if (this.animateRight) {
        this.animateLeft = true;
        this.animateRight = false
      } else {
        this.animateLeft = false;
        this.animateRight = true
      }

    }
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}

.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  /* transition: transform 1s; */
}

.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}

.animate-left {
  /* transform: translateX(-150px); */
  animation: slide-left 1s ease-out forwards;
}

.animate-right {
  animation: slide-right 1s ease-out forwards;
  /* transform: translateX(150px); */
}
/* .v-enter-from{
  opacity: 0;
  transform: translateY(-30px);
} */
.para-enter-active{
  /* transition: all 0.5s ease-out */
  animation: slide-enter 1s ease-out;
}
/* .v-enter-to{
  opacity: 1;
  transform: translateY(0);
} */
/* .v-leave-to{
  opacity: 0;
  transform: translateY(-30px);
} */
.para-leave-active{
  /* transition: all 0.3s ease-out */
  animation: slide-leave 1s ease-in;
}
/* .v-leave-from{
  opacity: 1;
  transform: translateY(0);
} */

@keyframes slide-enter {
  from{
    opacity: 0;
    transform: translateY(-30px);
  }

  to{
    opacity: 1;
    transform: translateY(0);
  }
}
@keyframes slide-leave {
  from{
    opacity: 1;
    transform: translateY(0);
  }

  to{
    opacity: 0;
    transform: translateY(30px);
  }
}

@keyframes slide-right {
  0% {
    transform: translateX(0) scale(1);
  }

  25% {
    transform: translateX(37.5px) scale(1.25);
  }

  50% {
    transform: translateX(75px) scale(1.50);
  }

  75% {
    transform: translateX(112.5px) scale(1.25);
  }

  100% {
    transform: translateX(150px) scale(1);
  }

}

@keyframes slide-left {
  0% {
    transform: translateX(0) scale(1);
  }

  25% {
    transform: translateX(-37.5px) scale(1.25);
  }

  50% {
    transform: translateX(-75px) scale(1.50);
  }

  75% {
    transform: translateX(-112.5px) scale(1.25);
  }

  100% {
    transform: translateX(-150px) scale(1);
  }
}

</style>