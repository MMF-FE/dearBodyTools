<template>
  <n-notification-provider>
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </n-notification-provider>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { NNotificationProvider } from "naive-ui";
export default {
  name: "App",
  components: {
    HelloWorld,
    NNotificationProvider,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

@font-face {
  font-family: SuisseIntl-Black;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-Black.otf");
}
@font-face {
  font-family: SuisseIntl-BlackItalic;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-BlackItalic.otf");
}
@font-face {
  font-family: SuisseIntl-Bold;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-Bold.otf");
}
@font-face {
  font-family: SuisseIntl-BoldItalic;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-BoldItalic.otf");
}
@font-face {
  font-family: SuisseIntl-Book;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-Book.otf");
}
@font-face {
  font-family: SuisseIntl-BookItalic;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-BookItalic.otf");
}
@font-face {
  font-family: SuisseIntl-Light;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-Light.otf");
}
@font-face {
  font-family: SuisseIntl-LightItalic;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-LightItalic.otf");
}
@font-face {
  font-family: SuisseIntl-Medium;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-Medium.otf");
}
@font-face {
  font-family: SuisseIntl-MediumItalic;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-MediumItalic.otf");
}
@font-face {
  font-family: SuisseIntl-Regular;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-Regular.otf");
}
@font-face {
  font-family: SuisseIntl-SemiBold;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-SemiBold.otf");
}
@font-face {
  font-family: SuisseIntl-RegularItalic;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-RegularItalic.otf");
}
@font-face {
  font-family: SuisseIntl-SemiBoldItalic;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-SemiBoldItalic.otf");
}
@font-face {
  font-family: SuisseIntl-Thin;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-Thin.otf");
}
@font-face {
  font-family: SuisseIntl-ThinItalic;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-ThinItalic.otf");
}
@font-face {
  font-family: SuisseIntl-UltraLightItalic;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-UltraLightItalic.otf");
}
@font-face {
  font-family: SuisseIntl-UltraLight;
  src: url("https://yz-cdn.meimeifa.com/yz-private/upqn/font/SuisseIntl-UltraLight.otf");
}
</style>