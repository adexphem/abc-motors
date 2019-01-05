<template>
  <app-navigation></app-navigation>
</template>

<script>
import { StackNavigator } from "vue-native-router";
import { Icon } from "react-native-elements";

import MainScreen from "./src/screens/Main";
import NewMemberScreen from "./src/screens/NewMember";

const AppNavigation = StackNavigator(
  {
    Home: MainScreen,
    AddMember: NewMemberScreen
  },
  {
    initialRouteName: "Home"
  }
);
export default {
  components: { AppNavigation }
};
</script>