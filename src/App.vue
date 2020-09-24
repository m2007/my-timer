<template>
  <div id="app">
    <div class="container">
      <div class="timers-wrap">

        <Timer v-for="tkey of timersKeys" :key="tkey"></Timer>
        <div class="plate creater">
          <div class="creater__img icon" @click="create()">
            <div class="icon__plus-h"></div>
            <div class="icon__plus-v"></div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
    Timer: () => import('./components/Timer.vue')
  },
  data: () => ({
    timersKeys: []
  }),
  methods: {
    create() {
      this.timersKeys.push(this.timersKeys.length)
    }
  }
}
</script>

<style lang="scss">
$bgray: #353638;
$gray: #696969;
$lgray:#9E9E9E;

@font-face {
  font-family: 'Gotham Pro';
  src: local('Gotham Pro'),
  url('./assets/fonts/GothamPro.woff') format('woff'),
  url('./assets/fonts/GothamPro.eot') format('eot'),
  url('./assets/fonts/GothamPro.ttf') format('ttf');
    
}
#app {
  font-family: 'Gotham Pro';
  font-weight: normal;
  font-style: normal;
  font-size: 22px;
  line-height: 21px;
  color: $lgray;

  min-height: 100vh;
  background: $bgray;
  display: flex;
}
html{
  box-sizing: border-box;
}
*,
*::before,
*::after{
  box-sizing: inherit;
}
body{
  margin: 0;
  padding: 0;
}
.container {
  margin: 72px auto 0;
}
.plate{
  width: 225px;
  height: 120px;
  background: $gray;
}
.timers-wrap{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  row-gap: 45px;
  column-gap: 50px;
}
.creater {
  display: flex;
  &__img{
    cursor: pointer;
    margin: auto;
  }
}

.icon{
  height: 20px;
  width: 20px;
  position: relative;

  &__trg{
    left: 0;
    border: 10px solid transparent; border-left: 17px solid $lgray;
  }

  &__pause-l, &__pause-r{
    position: absolute;
    top: 0;
    width: 3px;
    height: 20px;
    background-color: white;
  }
  &__pause-l{
    left: 5px;
  }
  &__pause-r{
    right: 5px;
  }

  &__square{
    width: 100%;
    height: 100%;
    background: $lgray;
  }

  &__plus-h, &__plus-v{
    position: absolute;
    background-color: $lgray;
  }
  &__plus-h{
    top: 8.5px;
    width: 20px;
    height: 3px;
  }
  &__plus-v{
    left: 8.5px;
    width: 3px;
    height: 20px;
  }
}

.clrw{
  color: white !important;
}
.brdclrw{
  border-bottom-color: white !important;
}
.bgrclrw{
  background-color: white !important;
}

@media screen and (max-width: 768px) {
    .timers-wrap{
      grid-template-columns: 1fr 1fr;
    }
}
@media screen and (max-width: 320px) {
    .timers-wrap{
      grid-template-columns: 1fr;
    }
}
</style>
