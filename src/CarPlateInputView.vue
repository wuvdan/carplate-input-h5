<script>

export default {
  data() {
    return {
      showCarPlate: false,
      inputIndex: 1,
      provinceArray: [
        ['皖','京','津','渝','沪','冀','晋','辽','吉'],
        ['黑','苏','浙','闽','赣','鲁','豫','鄂','湘'],
        ['粤','琼','川','贵','云','陕','甘','青'],
        ['蒙','桂','宁','新','藏']
      ],
      letterNumberAndCharacter: [
        ['1','2','3','4','5','6','7','8','9','0'],
        ['Q','W','E','R','T','Y','U','I','O','P'],
        ['A','S','D','F','G','H','J','K', 'L'],
        ['Z','X','C','V','B', 'N', 'M'],
        ['港', '澳', '学']
      ],
      carPlateArray: ['皖', 'A', '', '', '', '', '', '']
    }
  },

  methods: {
    getCarplateString() {
      return this.carPlateArray.join(',').replace(/\,/g, '')
    },

    hidenKeyboard() {
      this.showCarPlate = false
    },

    didTappedInputItem(index) {
      this.inputIndex = index;
      this.showCarPlate = true
    },

    didTappedKeyboard(item) {
      this.carPlateArray[this.inputIndex] = item
      if (this.inputIndex < 7) {
        this.inputIndex ++
      } else {
        this.showCarPlate = false
      }
    },

    didTappedKeyboardBox() {

    },

    didTappedDeleteButton() {
      this.carPlateArray[this.inputIndex] = ""
      this.inputIndex --
      if (this.inputIndex < 0) {
        this.inputIndex = 0
      }
    }
  }
}
</script>

<template>
 <div>
   <div class="wd-carplate-input-row">
     <div v-for="(item, index) in carPlateArray"  @click.stop="didTappedInputItem(index)" :class="[inputIndex === index ? 'wd-carplate-input-item-selected' : 'wd-carplate-input-item']">
       <div v-if="index === 7">
         <div v-if="item.length === 0" style="color: #3D75EF; font-size: 2.2vw">新能源</div>
         <div v-else>{{item}}</div>
       </div>
       <div v-else>{{item}}</div>
     </div>
   </div>

   <transition name="fullscreen"
     <div @click.stop="didTappedKeyboardBox" v-show="showCarPlate" class="wd-carplate-box">
       <div style="display: flex; align-items: center; justify-content: space-between;">
         <div></div>
         <div @click="showCarPlate = false" style="font-size: 4.5vw; color: #333333; margin: 0 2vw; padding-top: 1vw;">完成</div>
       </div>
       <div class="wd-carplate-column">
         <div v-if="inputIndex === 0" v-for="(item, index) in provinceArray" class="wd-carplate-row-box-province" :style="{gridTemplateColumns: `repeat(${item.length}, auto)`, marginBottom: `${index != 3 ? '3vw' : '0'}`}">
           <div v-for="child in item" @click.stop="didTappedKeyboard(child)" class="wd-carplate-button">{{child}}</div>
         </div>
         <div v-if="inputIndex === 1" v-for="(item, index) in letterNumberAndCharacter" class="wd-carplate-row-box" :style="{gridTemplateColumns: `repeat(${item.length}, auto)`, marginBottom: `${index != 4 ? '3vw' : '0'}`}">
           <div v-for="child in item">
             <div class="wd-carplate-button" v-if="(index === 0 || index === 4) || (child  === 'O')" style="color: #e2e2e2">{{child}}</div>
             <div class="wd-carplate-button" v-else @click.stop="didTappedKeyboard(child)">{{child}}</div>
           </div>
         </div>
         <div v-if="inputIndex === 6 || inputIndex === 7" v-for="(item, index) in letterNumberAndCharacter" class="wd-carplate-row-box" :style="{gridTemplateColumns: `repeat(${item.length}, auto)`, marginBottom: `${index != 4 ? '3vw' : '0'}`}">
           <div v-for="(child, childIndex) in item">
             <div class="wd-carplate-button" v-if="(child  === 'I' || child  === 'O')" style="color: #e2e2e2">{{child}}</div>
             <div class="wd-carplate-button" v-else @click.stop="didTappedKeyboard(child)">{{child}}</div>
           </div>
         </div>
         <div v-if="inputIndex < 6 && inputIndex > 1" v-for="(item, index) in letterNumberAndCharacter" class="wd-carplate-row-box" :style="{gridTemplateColumns: `repeat(${item.length}, auto)`, marginBottom: `${index != 4 ? '3vw' : '0'}`}">
           <div v-for="(child, childIndex) in item">
             <div class="wd-carplate-button" v-if="index === 4 || (child  === 'I' || child  === 'O')" style="color: #e2e2e2">{{child}}</div>
             <div class="wd-carplate-button" v-else @click.stop="didTappedKeyboard(child)">{{child}}</div>
           </div>
         </div>
         <div @click="didTappedDeleteButton" class="wd-carplate-delete-button">
           <div class="wd-carplate-delete-button-box">
             <svg class="icon" viewBox="0 0 1365 1024" p-id="7479"><path d="M452.355314 852.318871c5.347258 5.46103 10.694517 10.808288 19.284262 19.113605 4.26643 4.437087 8.589745 8.646631 14.619632 14.392089 1.649686 1.535915 1.991 1.877229 5.85923 5.973002l2.844286 2.901172a160.247097 160.247097 0 0 0 87.888451 44.939726c18.544748 3.128715 37.260152 4.778401 56.658186 5.005944a2368.323538 2368.323538 0 0 0 27.418921 0.568857h335.113827V1023.943114l-0.056886-39.364924v-39.42181h33.790123c7.45203 0 13.595689-0.113771 27.987778-0.511971 18.77229-0.227543 37.601467-1.877229 56.146214-4.949059 16.553747-2.787401 32.595522-8.077773 47.613355-15.700461 14.847175-7.565802 28.442864-17.407033 40.104439-29.125493 11.832232-11.946003 21.787234-25.598578 29.29615-40.047553 7.565802-15.18849 12.91306-31.400922 15.757347-47.784012 3.014944-18.544748 4.66463-37.317038 4.892173-56.771957 0.341314-10.239431 0.455086-19.056719 0.455085-27.475807V317.991223v-16.326204l-0.056885-7.167602a1125.029054 1125.029054 0 0 0-0.3982-21.44592 378.005666 378.005666 0 0 0-4.835287-55.748014 160.531526 160.531526 0 0 0-133.05572-133.055719 343.589801 343.589801 0 0 0-56.544414-4.949058c-13.766346-0.3982-19.910005-0.568857-27.305149-0.568858h-369.017722c-4.892173 0-10.011888 0.113771-16.155547 0.227543l-12.11666 0.341315a339.266485 339.266485 0 0 0-55.748014 4.949058 162.693184 162.693184 0 0 0-88.741736 45.736126c-4.209544 4.493973-5.916116 6.25743-7.338259 7.622687a540.414421 540.414421 0 0 0-15.928004 15.529804c-8.532859 8.419088-13.368146 13.197489-18.886062 18.829176L319.128937 304.907505a49.319927 49.319927 0 0 0-3.982001 3.583801l-3.071829 3.071829a500.253097 500.253097 0 0 0-12.799289 12.742404L181.465474 442.002111l-2.446086 2.446086-2.673629 2.67363-5.802345 5.85923a187.552247 187.552247 0 0 0-7.793345 8.077773 284.428643 284.428643 0 0 0-24.63152 27.077607l-2.844286 3.242486a24.290206 24.290206 0 0 0-4.26643 5.85923 54.724071 54.724071 0 0 0 0 29.466808 29.69435 29.69435 0 0 0 4.778401 6.769402c9.329259 11.206489 17.17949 19.853119 25.769235 28.442864l2.389201 2.332315 2.275429 2.275429a730.298983 730.298983 0 0 0 10.239431 10.410088l5.46103 5.46103 117.070829 117.298372 11.490918 11.149603 7.622687 7.622688c1.422143 1.137715 2.673629 2.275429 3.982001 3.640686l130.268319 130.268319z m222.764513-536.261763a34.017666 34.017666 0 0 0-52.448642-5.46103 33.847008 33.847008 0 0 0-0.113772 47.670241l-0.682628 0.625743 153.250153 152.851952-147.390923 147.390923a34.131437 34.131437 0 0 0-5.688573 52.619299 33.96078 33.96078 0 0 0 47.784012 0.227543l0.568857 0.568857L823.136492 559.755569l152.908839 152.62441 0.3982-0.3982a33.847008 33.847008 0 1 0 42.948725-52.050442l-148.301094-148.130437 153.022609-153.079496-0.341314-0.3982a33.96078 33.96078 0 1 0-51.766013-43.460696l-149.040609 148.983723-147.902894-147.732237z m-410.487418 460.205544l-9.386145-9.272374-11.604689-11.377145-117.355258-117.525916a733.769013 733.769013 0 0 1-11.32026-11.377145 793.726571 793.726571 0 0 1-4.949058-5.005944l-4.26643-4.323316a416.232876 416.232876 0 0 1-28.158435-30.832065 108.424199 108.424199 0 0 1-19.511805-29.808121L56.658186 552.929282a133.453919 133.453919 0 0 1 0-81.915449l1.308371-3.583801c4.778401-10.978946 11.377146-21.04772 19.625577-29.751236 8.532859-10.637631 17.634576-20.706405 27.362035-30.206322a270.776068 270.776068 0 0 1 10.011888-10.353203l5.290373-5.347258 2.958058-3.014944 2.844287-2.844286 116.843286-116.615744c3.640687-3.86823 6.883173-7.110716 12.059774-12.11666 3.128715-3.185601 3.128715-3.185601 4.835287-4.778401a508.558413 508.558413 0 0 1 5.233487-5.119716l130.837176-130.609633c5.688573-5.85923 10.92206-11.035831 19.284262-19.227376 5.46103-5.574801 11.092717-11.092717 17.350147-17.008833 5.005944-5.290373 6.029887-6.428087 6.655631-6.940059A239.31826 239.31826 0 0 1 569.5968 6.598745c22.64052-3.86823 45.508583-5.916116 67.694017-6.086773A2429.248153 2429.248153 0 0 1 666.757625 0h368.960835c8.419088 0 15.074718 0.113771 28.727293 0.568857 22.981834 0.113771 45.906783 2.104772 68.376646 6.029888 24.460863 4.038887 48.239098 11.889117 70.253875 23.152491a239.773346 239.773346 0 0 1 104.157769 104.100883c11.092717 22.071663 18.886062 45.67924 23.152491 70.367647 3.640687 22.412977 5.631687 45.110383 5.85923 67.125159a1129.067941 1129.067941 0 0 1 0.511972 29.808122v421.63702c0 9.272374-0.170657 18.886062-0.455086 29.125493-0.284429 22.754291-2.275429 45.394811-6.029887 68.149103a253.141492 253.141492 0 0 1-23.209378 70.481418c-11.377146 22.014777-26.110549 42.209211-43.631353 59.900672-17.691462 17.634576-38.056552 32.424865-60.298873 43.745125a242.902061 242.902061 0 0 1-70.31076 23.152492 447.235598 447.235598 0 0 1-67.52336 6.086773c-14.505861 0.3982-21.161491 0.511972-29.580579 0.511971h-33.790123v-78.786734l0.056886 39.42181V1023.943114h-335.113827a764.145992 764.145992 0 0 1-29.011722-0.568857c-22.754291-0.227543-45.508583-2.275429-68.035331-6.029887a244.437976 244.437976 0 0 1-70.481418-23.152492 236.985945 236.985945 0 0 1-64.565302-48.295983l-2.275429-2.446087a643.662019 643.662019 0 0 1-16.610632-16.269318 1088.05333 1088.05333 0 0 1-19.625577-19.511805l-127.31026-127.253375-4.380201-4.152658z" fill="#3F434A" p-id="7480"></path></svg>
           </div>
         </div>
       </div>
       <div class="wd-carplate-safe-bottom"></div>
     </div>
   </transition>
 </div>
</template>

<style scoped>

.wd-carplate-safe-bottom {
  height: constant(safe-area-inset-bottom);
  height: env(safe-area-inset-bottom);
  background: #f5f5f5;
}

.wd-carplate-box {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  background: #f5f5f5;
  z-index: 99999999 !important;
}

.wd-carplate-delete-button {
  position: absolute;
  right: 3vw;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: white;
  color: #333333;
  font-size: 4.5vw;
  font-weight: 420;
  height: 10vw;
  width: 8vw;
  border-radius: 8px;
}

.wd-carplate-delete-button-box {
  height: 7.2vw;
  width: 6vw;
  display: flex;
  align-items: center
}

.wd-carplate-delete-button:active{
  background: #e2e2e2;
}

.wd-carplate-column {
  display: flex;
  align-items: center;
  flex-direction: column;
  position: relative;
  padding-top: 3vw;
  margin-bottom: 3vw;
}

.wd-carplate-row-box-province {
  display: grid;
  grid-column-gap: 10px;
}

.wd-carplate-row-box {
  display: grid;
  grid-column-gap: 1.7vw;
}

.wd-carplate-button {
  display: flex;
  align-items: center;
  justify-content: center;
  background: white;
  color: #333333;
  font-size: 4.5vw;
  font-weight: 420;
  height: 10vw;
  width: 8vw;
  border-radius: 4px;
}

.wd-carplate-button:active{
  background: #e2e2e2;
}

.wd-carplate-input-row {
  display: grid;
  grid-template-columns: repeat(8, auto);
}

.wd-carplate-input-item {
  border-radius: 4px;
  border: solid 1px #e2e2e2;
  width: 8vw;
  height: 10vw;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 4.7vw;
}

.wd-carplate-input-item-selected {
  border-radius: 4px;
  border: solid 1px #3D75EF;
  width: 8vw;
  height: 10vw;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 4.7vw;
}

.fullscreen-enter{
  animation:fullscreen-dialog-fade-in 0.4s ease;
}

.fullscreen-leave{
  animation:fullscreen-dialog-fade-out 0.4s ease forwards;
}

.fullscreen-enter-active{
  animation:fullscreen-dialog-fade-in 0.4s ease
}

.fullscreen-leave-active{
  animation:fullscreen-dialog-fade-out 0.4s ease forwards
}

@keyframes fullscreen-dialog-fade-in {
  0% {
    transform: translate3d(0, 100%, 0);
    opacity: 1;
  }
  100% {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
}

@keyframes fullscreen-dialog-fade-out {
  0% {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
  100% {
    transform: translate3d(0, 100%, 0);
    opacity: 1;
  }
}
</style>
