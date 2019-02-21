<template>
  <div class="home" :style="bgpos">
    <textWidget>
      Which planet
      would you like to
      explore?
    </textWidget>
    <planetSelection @position-update="posUpdate"/>
  </div>
</template>

<style lang="scss" scoped>
.home {
  width: 100%;
  height: 100%;
  display: flex;
  background-image: url('../assets/bg.jpg');
  background-color: #000;
  background-blend-mode: luminosity;
  background-size: cover;
  transition: all 0.3s;

}
</style>


<script>
// @ is an alias to /src
import textWidget from '@/components/textWidget.vue'
import planetSelection from '@/components/planetSelection.vue'

export default {
  name: 'home',
  components: {
    textWidget,
    planetSelection
  },
  data: function(){
    return {
      bgpos: {
        backgroundPosition: '0%',
        backgroundColor: "red",

      }
    }
  },
  methods: {
    posUpdate: function(plan_data){
      let pos_pc = plan_data[0];
      let planetData = plan_data[1]
      this.bgpos.backgroundPosition = pos_pc.toString()+'%';
      this.bgpos.backgroundColor = planetData.bg_img_color.backgroundColor;
    }
  }
}
</script>
