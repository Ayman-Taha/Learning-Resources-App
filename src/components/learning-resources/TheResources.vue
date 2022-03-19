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
  <keep-alive>
    <component :is="activeTab"></component>
  </keep-alive>
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
    pushResource(id, title, description, link) {
      const newResource = {
        id: id,
        title: title,
        description: description,
        link: link,
      };

      this.resources.unshift(newResource);
      this.changeTab('stored-resources');
    },
  },
  provide() {
    return { resources: this.resources, pushResource: this.pushResource };
  },
};
</script>

<style></style>
