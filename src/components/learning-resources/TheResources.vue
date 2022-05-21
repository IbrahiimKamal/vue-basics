<template>
  <base-card v-if="storedResources.length">
    <base-button
      @click="setSelectTab('stored-resources')"
      :mod="storedResButtonMod"
    >
      Stored Resources</base-button
    >
    <base-button @click="setSelectTab('add-resource')" :mod="addResButtonMod"
      >Add Resource</base-button
    >
  </base-card>

  <h3 v-else>No Items Found!</h3>

  <base-card>
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
import BaseCard from '../UI/BaseCard.vue';
import AddResource from './AddResource.vue';
import StoredResources from './StoredResources.vue';

export default {
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 1,
          title: 'Learn Vue.js',
          description: 'This is the first resource',
          link: 'https://vuejs.org/',
        },
        {
          id: 2,
          title: 'Resource 2',
          description: 'This is the second resource',
          link: 'https://vuejs.org/',
        },
      ],
    };
  },

  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource,
    };
  },

  computed: {
    storedResButtonMod() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMod() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },

  methods: {
    setSelectTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      this.storedResources.unshift({
        id: this.storedResources.length + 1,
        title,
        description,
        link: url,
      });
      this.selectedTab = 'stored-resources';
    },
    deleteResource(id) {
      const resIndex = this.storedResources.findIndex((res) => res.id === id);
      this.storedResources.splice(resIndex, 1);
    },
  },

  components: {
    BaseButton,
    BaseCard,
    StoredResources,
    AddResource,
  },
};
</script>
