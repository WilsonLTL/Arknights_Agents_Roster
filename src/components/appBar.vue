<template>
  <v-app-bar
    :collapse="!collapseOnScroll"
    :collapse-on-scroll="collapseOnScroll"
    absolute
    color="blue-grey darken-3"
    dark
    scroll-target="#scrolling-techniques-6"
  >
    <v-app-bar-nav-icon>
      <v-avatar>
        <img src="https://aceship.github.io/AN-EN-Tags/img/factions/logo_rhodes.png" />
      </v-avatar>
    </v-app-bar-nav-icon>

    <v-toolbar-title>明日方舟幹員名冊 - Arknights Agents Roster </v-toolbar-title>

    <div class="flex-grow-1"></div>

    <v-avatar id="pwa">
      <img
        src="https://upload.wikimedia.org/wikipedia/zh/thumb/5/5d/%E6%98%8E%E6%97%A5%E6%96%B9%E8%88%9F%E6%89%8B%E6%A9%9F%E9%81%8A%E6%88%B2LOGO.png/220px-%E6%98%8E%E6%97%A5%E6%96%B9%E8%88%9F%E6%89%8B%E6%A9%9F%E9%81%8A%E6%88%B2LOGO.png"
      />
    </v-avatar>
  </v-app-bar>
</template>
<script>
export default {
  name: "appBar",
  data: () => ({
    collapseOnScroll: true
  })
};
</script>