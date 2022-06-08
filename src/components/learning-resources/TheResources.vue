<template>
  <base-card>
    <base-button :mode='storedResButtonMode' @click='setSelectedTab("stored-resources")'>
      Stored Resources
    </base-button>
    <base-button :mode='addResButtonMode' @click='setSelectedTab("add-resource")'>
      Add Resources
    </base-button>
  </base-card>
  <keep-alive>
    <component :is='selectedTab'></component>
  </keep-alive>

</template>

<script>
import StoredResources from '@/components/learning-resources/StoredResources';
import AddResource from '@/components/learning-resources/AddResource';
import BaseCard from '@/components/UI/BaseCard';
import BaseButton from '@/components/UI/BaseButton';

export default {
  components: {
    StoredResources,
    AddResource,
    BaseCard,
    BaseButton
  },
  name: 'TheResources',
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org'

        },
        {
          id: 'google',
          title: 'Google',
          description: 'Gooogling is  must',
          link: 'https://google.com'
        }
      ]
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, desc, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: desc,
        link: url
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    }
  }
};
</script>

<style scoped>

</style>
