<template>
  <ScrollView class="coverage">
    <ImageBackground v-bind:source="bgImage" :style="{width: '100%', height: '100%'}">
      <text :on-press="goBack" class="_back white-bg full-width">Back</text>
    </ImageBackground>
  </ScrollView>
</template>

<script>
import bgImg from "../../assets/bgImg.jpeg";

export default {
  name: "NewMember",
  props: {
    navigation: {
      type: Object
    }
  },
  data() {
    return {
      bgImage: bgImg
    };
  },
  methods: {
    goBack() {
      this.navigation.goBack();
    }
  },
  componentDidMount() {}
};
</script>

<style scoped>
._back {
  width: 100%;
  font-size: 15;
  text-align: center;
  padding: 15;
}

.coverage {
  flex: 1;
  flex-direction: row;
  align-items: stretch;
  width: 100%;
  height: 100%;
}

.full-width {
  width: 100%;
  height: 50;
}

.white-bg {
  background: #f0f0f0;
}
</style>
