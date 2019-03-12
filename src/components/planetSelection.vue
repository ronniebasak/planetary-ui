<template>
  <div id="planet-selection" :class="{selected : isSelected}">

    <template v-for="(planet, ind) in planet_data">
      <!-- left offscreen -->
    <div :key="planet.name" v-if="ind<pos-1" class="planet" data-bg="planet_data[pos-1].image">
      <img :src="require(`@/assets/${planet.image}`)" alt class="planet-image">
      <span class="planet-name">{{ planet.name }}</span>
    </div>

    <!-- previous one -->
    <div :key="planet.name" v-if="ind==pos-1" class="planet prev-planet" data-bg="planet_data[pos-1].image"
    @click="prevPlanet">
      <img :src="require(`@/assets/${planet.image}`)" alt class="planet-image">
      <span class="planet-name">{{ planet.name }}</span>
    </div>

    <!-- current one -->
    <div :key="planet.name" v-if="ind==pos" class="planet current-planet" @click="selectPlanet">
      <img :src="require(`@/assets/${planet.image}`)" alt class="planet-image">
      <span class="planet-name">{{ planet.name }}</span>
    </div>

    <!-- next one -->
    <div :key="planet.name" v-if="ind==pos+1" class="planet next-planet" data-bg="planet_data[pos-1].image"
    @click="nextPlanet" >
      <img :src="require(`@/assets/${planet.image}`)" alt class="planet-image">
      <span class="planet-name">{{ planet.name }}</span>
    </div>

    <!-- remaining -->
    <div :key="planet.name" v-if="ind>pos+1" class="planet offscreen-right" data-bg="planet_data[pos-1].image">
      <img :src="require(`@/assets/${planet.image}`)" alt class="planet-image">
      <span class="planet-name">{{ planet.name }}</span>
    </div>
    </template>

    <div class="planet-highlight" :style="planet_data[pos].bg_style"></div>

    <div class="planet-description"> {{ planet_data[pos].description }} </div>

    <!-- <button @click="nextPlanet">np</button> -->
  </div>
</template>

<style lang="scss" scoped>
#planet-selection {
  width: 100%;
  align-self: center;
  justify-self: center;
  height: 60%;
  display: flex;
  align-items: center;
  --planet-size: 20vw;
  --hl-planet-size: 40vw;
  overflow: hidden;
  position: relative;
}


.planet {
  position: absolute;
  width: var(--planet-size);
  height: var(--planet-size);
//   opacity: 0;
  transition: all 0.3s ease-in-out;
  z-index: 1000;
  margin-left: -105vw;
}

.prev-planet {
  width: var(--planet-size);
  height: var(--planet-size);

  margin-left: calc(
    (((100vw - var(--hl-planet-size)) / 2) - var(--planet-size)) / 2
  );
}

.current-planet {
  width: var(--hl-planet-size);
  height: var(--hl-planet-size);
  margin-left: calc((100vw - var(--hl-planet-size)) / 2);
  z-index: 1000;
}

.next-planet {
  width: var(--planet-size);
  height: var(--planet-size);
  margin-left: calc(
    50vw + (var(--hl-planet-size) / 2) +
      calc((((100vw - var(--hl-planet-size)) / 2) - var(--planet-size)) / 2)
  );
}

.offscreen-right {
    width: var(--planet-size);
    height: var(--planet-size);

    margin-left: 105vw;
}


.planet-highlight {
  position: absolute;
  width: calc(var(--hl-planet-size) + 4vw);
  height: calc(var(--hl-planet-size) + 4vw);
  margin-left: calc((100vw - 42vw) / 2 - 1vw);
  border-radius: 4000px;
  z-index: 900;
  transition: all 0.3s ease-in-out;
}


.planet > .planet-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
}

.planet > .planet-name {
  color: white;
  top: calc(var(--planet-size) + 30%);
  position: relative;
  font-weight: bold;
  text-transform: uppercase;
  font-size: 1em;
  font-family: "Open Sans";
  transition: all 0.3s;
}


.current-planet > .planet-name {
  top: calc(var(--planet-size) + 75%);
  font-size: 2em;
}

.planet-description {
  color: transparent;
  font-size: 1.5em;
  padding: 30px;
  text-align: center;
  z-index: 950;
  margin-top: 490%;
  transition: all 0.3s ease-in-out;
}

.selected {
  &#planet-selection {
    height: 100%;
  }

  & .current-planet {
    margin-top: -50%;
    --hl-planet-size: 60vw;

  }

  & .prev-planet {
    margin-left: -105vw;
  }

  & .next-planet {
    margin-left: 105vw;
  }

  & .current-planet > .planet-name {
    font-size: 3em;
  }

  & .planet-highlight {
    width: 100vmax;
    height: 100vmax;
    border-radius: 0;
    margin-left: 0;
  }

  & .planet-description {
    margin-top: 100%;
    color: white;
  }
}
</style>


<script>
import planets from "@/assets/planet-desc.js";
export default {
  name: "planetSelection",
  props: {},
  data: function() {
    return {
      planet_data: planets,
      pos: 3,
      isSelected: false,
    };
  },
  created: function(){
      this.$emit('position-update', [(this.pos/this.planet_data.length)*100, this.planet_data[this.pos]] );
  },
  methods: {
    nextPlanet: function() {
      this.pos++;
      this.$emit('position-update', [(this.pos/this.planet_data.length)*100, this.planet_data[this.pos]] );
    },
    prevPlanet: function(){
      this.pos--;
      this.$emit('position-update', [(this.pos/this.planet_data.length)*100, this.planet_data[this.pos]] );

    },
    selectPlanet: function() {
      this.isSelected = !this.isSelected;
    }
  }
};
</script>
