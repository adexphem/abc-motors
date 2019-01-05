<template>
  <text :on-press="goBack" class="_back">Back</text>
</template>

<script>
export default {
  name: "NewMember",
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    goBack() {
      this.navigation.goBack();
    }
  },
  componentDidMount() {}
};
</script>

<style>
._back {
  width: 100%;
  font-size: 15;
  text-align: center;
  padding: 15;
}
</style>
