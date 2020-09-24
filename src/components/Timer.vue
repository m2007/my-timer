<template>
  <div class="plate timer">
    <div class="timer__clock" :class="this.state == 'play' ? 'clrw brdclrw' : ''">
      <div class="timer__clock-numbers">
        {{displayTime}}
      </div>
    </div>
    <div class="timer__controller">
      <div class="timer__pl-ps" @click="playStart()">

        <div class="icon" v-if="state == 'pause'">
          <div class="icon__trg"></div>
        </div>

        <div class="icon" v-else>
          <div class="icon__pause-l" ></div>
          <div class="icon__pause-r" ></div>
        </div>

      </div>
      
      
      <div class="timer__reset" @click="reset()">
        <div class="icon">
          <div class="icon__square" :class="this.state == 'play' ? 'bgrclrw' : ''"></div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'Timer',
  data: () => ({
    reseted: true,
    state: 'pause',
    whenStarted: 0,
    time: 0,
    whenPaused: 0,
    timePaused: 0,
    id: null
  }),
  computed: {
    displayTime() {
      let allSecs = Math.floor(this.time)

      let h = Math.floor(allSecs / 3600).toString()

      let m = (Math.floor(allSecs / 60) - h * 60).toString()
      if (+h) m = m.padStart(2, "0")

      let s = (allSecs - h * 3600 - m * 60).toString()
      if (+h || +m) s = s.padStart(2, "0")

      return (h != 0) ? (h + ':' + m + ':' + s) : (m != 0 ? (m + ':' + s) : s)
    }
  },
  methods: {
    updateTime() {
      this.time = (new Date().getTime() - this.whenStarted - this.timePaused) / 1000
    },
    playStart() {
      if (this.state == 'pause') {
        this.state = 'play'

        let now = new Date().getTime()
        if (this.reseted) this.whenStarted = now
        else this.timePaused += (now - this.whenPaused)
        
        this.updateTime()
        this.id = setInterval(() => {this.updateTime()}, 100)

        this.reseted = false
      } else {
        this.state = 'pause'

        clearInterval(this.id)
        this.id = null
        
        this.whenPaused = new Date().getTime()
      }
    },
    reset() {
      clearInterval(this.id)
      this.id = null
      this.reseted = true
      this.time = 0
      this.timePaused = 0
      this.state = 'pause'
    }
  }
}
</script>

<style lang="scss">
.timer{
  &__clock{
    border-bottom: 1px solid #9E9E9E;
  }
  &__controller{
    justify-content: center;
    align-items: center;
  }
  &__pl-ps, &__reset{
    cursor: pointer;
  }
  &__pl-ps{
    margin-right: 50px;
  }
  &__clock, &__controller{
    display: flex;
    width: 100%;
    height: 50%;
  }
  &__clock-numbers{
    margin: auto;
  }
}
</style>
