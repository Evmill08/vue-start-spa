<template>
    <div class="container">
        <h1 class="emphasize">{{page.pageTitle}}</h1> <!--These are essentially placeholders for what Vue instance returns-->
        <p>{{page.content}}</p>
    </div>

</template>

<script>
    export default{
        props: {
            page: { // How we can validate the page, giving the default values if pages isnt loaded yet
                type: Object,
                default(rawProps){
                    return {
                        pageTitle: "",
                        content: ""
                    };
                }
            }
        }  
    }
</script>

<style scoped>
.emphasize {
    color: blue;
}
</style>