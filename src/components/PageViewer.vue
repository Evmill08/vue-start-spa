<template>
    <div v-if="page" class="container">
        <h1 class="emphasize">{{ page.pageTitle }}</h1> <!--These are essentially placeholders for what Vue instance returns-->
        <p>{{page.content}}</p>
    </div>

</template>

<script>
    export default{
        props: ['index'],
        created() {
            this.page = this.$pages.getSinglePage(this.index);
            
            // this.$watch(() => this.$route.params, (newParams, previousParams) => {
            //     this.page = this.$pages.getSinglePage(newParams);
            // });
        },

        data() {
            return {
                page: null
            }
        },
        watch: {
            index(newIndex, oldIndex){
                this.page = this.$pages.getSinglePage(this.index);
            }
        }
        
    }
</script>

<style scoped>
.emphasize {
    color: blue;
}
</style>