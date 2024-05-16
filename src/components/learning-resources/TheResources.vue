<template>
    <base-card>
    <!-- UX: these are the two tabs, the user can switch between the both -->
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
    </base-card>
    <!-- keep-alive component allows entered text not to be lost when switching between tabs -->
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
    components: {
        StoredResources,
        AddResource
    },
    data(){
        return {
            selectedTab: 'stored-resources', // this is not a string, it refers to a component key name us in the DOM, with the <component> tag
            storedResources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js documentation.',
                    link: 'https://vuejs.org',
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'Learn to google...',
                    link: 'https://google.org',
                },
            ],
        };
    },
    computed: {
        // this computed property's modifying the style of the base-button: highlight the choice the user made when clicking on one tab
        storedResButtonMode() {
            return this.selectedTab ==='stored-resources' ? null : 'flat'
        },
        addResButtonMode() {
            return this.selectedTab ==='add-resource' ? null : 'flat'
        }
    },
    provide(){
        return {
           resources : this.storedResources,
           addResource: this.addResource,
           deleteResource: this.removeResource
        };
    },
    methods: {
        // make the switch between tabs
      setSelectedTab(tab) {
        this.selectedTab = tab;
      },
      addResource(title, description, url) {
        const newResource = {
            id: new Date().toISOString(),
            title: title,
            description: description,
            link: url
        };
        this.storedResources.unshift(newResource);
        this.selectedTab = 'stored-resources';
      },
      removeResource(id) {
        // I use this way to delete, in another case (with .filter()) I was deleting a resource from a duplicated array, not the orignal one
        const resIndex = this.storedResources.findIndex(res => res.id === id);
        this.storedResources.splice(resIndex, 1);
      }
    }
}    
</script>