<template>
  <div :class='{wavey: anime.wavey}'>
    <div :class='{spining: anime.spining}'>
      <div ref='box'
        @mouseover='mouseover'
        @mouseleave='mouseleave'
        @click='click'
        class='body'
      >
        {{ kaomoji }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      state: '',
      action: '',
      kaomoji: '',
      anime: {
        hidden: true,
        spining: false,
        wavey: true,
      }
    }
  },
  mounted() {
    setTimeout(() => {
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
          this.anime.spining = true
          setTimeout(() => {
            this.anime.spining = false
            this.kaomoji = '(´｡• ω •｡`)'
          }, 1000)
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

div {
  position: absolute;

  display: grid;
  justify-items: center;
  align-items: center;
}

.body {
  width: 300px;
  height: 200px;

  font-family: monospace;
  font-size: 50px;
  font-weight: bolder;

  border: 10px solid #045d5c;
  border-radius: 30px;

  background: #cceeff;

  box-shadow: 10px 10px 0px #00000030;

  user-select: none;
}

.hidden {
  animation: hidden 2s linear;
}

.wavey {
  animation: wavey 2s ease-in-out infinite;
}

.spining {
  animation: spining 0.5s ease-in-out;
}

@keyframes hidden {
  0% {
    opacity: 0;
    transform: translate(-200px, -200px) scale(0);
  }
  100% {
    opacity: 1;
    transform: translate(0%, 0%) scale(1);
  }
}

@keyframes wavey {
  0% {
    transform: translate(-10px, -10px);
  }
  50% {
    transform: translate(10px, 10px);
  }
  100% {
    transform: translate(-10px, -10px);
  }
}

@keyframes spining {
  0% {
    transform: rotate(0)
  }
  100% {
    transform: rotate(360deg)
  }
}

</style>