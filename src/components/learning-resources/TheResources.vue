<template>
  <base-card>
    <base-button
      @click="changeTab('stored-resources')"
      :mode="storedResourcesButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="changeTab('add-resource')"
      :mode="addResourceButtonMode"
      >Add Resource</base-button
    >
  </base-card>
  <component :is="activeTab"></component>
</template>

<script>
import AddResource from './AddResource.vue';
import StoredResources from './StoredResources.vue';
export default {
  components: { AddResource, StoredResources },
  data() {
    return {
      activeTab: 'stored-resources',
      resources: [
        {
          id: 'google',
          title: 'Google',
          description: 'google to search',
          link: 'https://www.google.com/',
        },
        {
          id: 'vue3',
          title: 'Vue 3',
          description: 'learn Vue.js',
          link: 'https://vuejs.org/',
        },
      ],
    };
  },
  computed: {
    storedResourcesButtonMode() {
      return this.activeTab === 'stored-resources' ? null : 'flat';
    },
    addResourceButtonMode() {
      return this.activeTab === 'add-resource' ? null : 'flat';
    },
  },
  methods: {
    changeTab(tab) {
      this.activeTab = tab;
    },
  },
  provide() {
    return { resources: this.resources };
  },
};
</script>

<style></style>
