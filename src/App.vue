<template>
  <the-header :title="title"></the-header>
  <stored-resources :storedResources="resources"></stored-resources>
</template>

<script>
import TheHeader from './components/layout/TheHeader.vue';
import StoredResources from './components/learning-resources/StoredResources.vue';
export default {
  components: { StoredResources, TheHeader },
  data() {
    return {
      title: 'Remember Me',
      resources: [
        {
          id: 'google',
          title: 'Google',
          description: 'google to search',
          link: 'www.google.com',
        },
        {
          id: 'vue3',
          title: 'Vue 3',
          description: 'learn Vue.js',
          link: 'www.vue.com',
        },
      ],
    };
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}
</style>
