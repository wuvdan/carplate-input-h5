<template>
  <div id="app" @click="keyboardHiden">
	  <car-plate-input-view ref="keyboard"></car-plate-input-view>
    <div style="margin-top: 100px">
      <div @click.stop="getCarplate">获取车牌</div>
      <div v-if="carplateString">{{carplateString}}</div>
    </div>
  </div>
</template>

<script>
import carPlateInputView from "@/CarPlateInputView.vue";

export default {
  name: 'app',
  components: {
    carPlateInputView
  },
  data() {
    return {
      wdViewShow: false,
      carplateString: ""
    }
  },
  methods: {
    keyboardHiden() {
      this.$refs.keyboard.hidenKeyboard()
    },

    getCarplate() {
      this.carplateString = this.$refs.keyboard.getCarplateString()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  min-height: 100vw;
}

</style>
