<template>
  <app-navigation></app-navigation>
</template>

<script>
import { StackNavigator } from "vue-native-router";

import MainScreen from "./src/screens/Main";
import NewMemberScreen from "./src/screens/NewMember";

const AppNavigation = StackNavigator(
  {
    Home: {
      screen: MainScreen,
      navigationOptions: {
        title: "Member List",
        headerStyle: {
          backgroundColor: "#ffffff"
        }
      }
    },
    AddMember: {
      screen: NewMemberScreen,
      navigationOptions: {
        title: "New Member",
        headerStyle: {
          backgroundColor: "#ffffff"
        }
      }
    }
  },
  {
    initialRouteName: "Home"
  }
);
export default {
  components: { AppNavigation }
};
</script>

<style>
.flex {
  display: flex;
}

.coverage {
  flex: 1;
  align-items: center;
  justify-content: center;
}
</style>