<template>
  <NavBar />
  <div class="row">
    <div class="col-2">
      <div class="list-group">
        <router-link
          :to="{ name: 'FormatJSON' }"
          class="list-group-item list-group-item-action"
          :class="{ active: $route.name === 'FormatJSON' }"
          >Format JSON</router-link
        >
        <a href="#" class="list-group-item list-group-item-action">More tools coming soon..</a>
      </div>
    </div>
    <div class="col-10 tool-container">
      <router-view />
    </div>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar.vue';

export default {
  components: {
    NavBar,
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
}
* {
  box-sizing: border-box;
}
body {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
#app {
  height: 100%;
  width: 100%;
}
.tool-container {
  overflow: auto;
}
</style>
