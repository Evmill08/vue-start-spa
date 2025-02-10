<template>
    <navbar 

    ></navbar>

    <router-view>

    </router-view>

    <!--<page-viewer 
        v-if="pages.length > 0"
        :page="pages[activePage]">
    </page-viewer>

    <create-page
        @page-created="pageCreated"
    ></create-page>-->

</template>

<script>
    import PageViewer from './components/PageViewer.vue';
    import Navbar from './components/Navbar.vue';
    import CreatePage from './components/CreatePage.vue';
    import { RouterView } from 'vue-router';


    export default{
        components: {
            Navbar,
        },
        
        methods: {
            pageCreated(pageObj) {
                this.pages.push(pageObj);
            }
        }
    }
</script>