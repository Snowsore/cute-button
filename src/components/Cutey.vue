<template>
  <div ref='box'
    @mouseover='mouseover'
    @mouseleave='mouseleave'
    @click='click'
    class='body hidden'
  >
    {{ kaomoji }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      state: '',
      action: '',
      kaomoji: '',
    }
  },
  mounted() {
    setInterval(() => {
      this.$refs.box.classList.remove('hidden')
      this.step()
    }, 0)
  },
  methods: {
    mouseover() {
      this.action = 'mouseover'
      this.step()
    },
    mouseleave() {
      this.action = 'mouseleave'
      this.step()
    },
    click() {
      this.action = 'click'
      this.step()
    },
    step() {
      switch(this.state) {
        case 'happy': 
          switch(this.action) {
            case 'mouseover':
              this.state = 'omg'
              break
          }
          break
        case 'omg':
          switch(this.action) {
            case 'mouseleave':
              this.state = 'happy'
              break
            case 'click':
              this.state = 'shy'
              break
          }
          break
        case 'shy':
          switch(this.action) {
            case 'mouseover':
              this.state = 'omg'
              break
          }
          break
        default:
          this.state = 'happy'
      }

      switch(this.state) {
        case 'happy':
          this.kaomoji = '(´｡• ω •｡`)'
          break
        case 'omg':
          this.kaomoji = '(ﾟωﾟ；)'
          break
        case 'shy':
          this.kaomoji = '(*ﾟдﾟ*)'
          break
        default:
          this.kaomoji = 'X_X'
      }
    }
  }
}
</script>

<style scoped>

.body {
  position: absolute;

  width: 300px;
  height: 200px;

  display: grid;
  justify-items: center;
  align-items: center;

  font-family: monospace;
  font-size: 50px;
  font-weight: bolder;

  border: 10px solid #045d5c;
  border-radius: 30px;

  opacity: 1;

  background: #cceeff;

  box-shadow: 10px 10px 0px #00000030;

  transition: all 1s;
  transform: translate(0, 0) scale(1);
  transition-timing-function: ease-in;

  animation: wavey 2s ease-in-out infinite;
  animation-delay: 1s;

  user-select: none;
}

.hidden {
  opacity: 0;
  transform: translate(-200px, -200px) scale(0);
}

@keyframes wavey {
  
  0% {
    transform: translate(0%, 0%);
  }

  50% {
    transform: translate(10%, 10%);
  }

  100% {
    transform: translate(0%, 0%);
  }

}

</style>