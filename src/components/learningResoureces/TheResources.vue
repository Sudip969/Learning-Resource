<template>
    <base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="storeButtonMode">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode="addButtonMode">Add Resource</base-button>
    </base-card>
    <component :is="selectedTab"></component>
</template>

<script>
import StoredResources from './StoredResources'
import AddResource from './AddResource.vue'
export default{
    components:{StoredResources , AddResource},
    data(){
        return{
            selectedTab:"stored-resources",
            storedResources:[
        {
          id:"official-guide",
          title:"Official Guide",
          description:"The Official vue.js documentation ",
          link:"http://vuejs.org"
        },
        {
          id:"google",
          title:"Google",
          description:"Learn To Google",
          link:"http://www.google.com"
        }
      ]
    };
    },
    computed:{
        storeButtonMode(){
            return this.selectedTab==="stored-resources" ? null:"flat"
        },
        addButtonMode(){
            return this.selectedTab === "add-resource" ? null : "flat"
        }
    },
    provide(){
        return{
            resources:this.storedResources,
            addResource:this.addResource,
            removeResource:this.removeResource
        }
    },
    methods:{
        setSelectedTab(tab){
            this.selectedTab=tab;
        },
        addResource(title,description,link){
            const newResource={
                id:new Date().toISOString(),
                title:title,
                description:description,
                link:link
            }
            this.storedResources.unshift(newResource);
            this.selectedTab='stored-resources';
        },
        removeResource(resId){
            const resIndex= this.storedResources.findIndex(res=> resId===res.id)
            this.storedResources.splice(resIndex,1)
        }
    }
}
</script>
