<template>
    <form action="" class="container mb-3">
        <div class="row">
            <div class="col-md-8">
                <div class="mb-3">
                    <label for="" class="form-label">Page Title</label>
                    <input 
                    type="text" 
                    class="form-control"
                    v-model="pageTitle"
                    />
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">Content</label>
                    <textarea 
                    type="text" 
                    class="form-control" 
                    rows="5"
                    v-model="content"
                    ></textarea>
                </div>
            </div>
            <div class="col">
                <div class="mb-3">
                    <label for="" class="form-label">Link Text</label>
                    <input 
                        type="text"
                        class="form-control"
                        v-model="linkText"
                    />
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">Link URL</label>
                    <input 
                    type="text" 
                    class="form-control"
                    v-model="linkURL"
                    />
                </div>
                <div class="row mb-3">
                    <div class="form-check">
                        <input class="form-check-input" type="checkbox" v-model="published">
                        <label class="form-check-label" form="gridCheck1">Published</label>
                    </div>
                </div>
            </div>
        </div>

        <div class="mb-3">
            <button 
                class="btn btn-primary" 
                :disabled="isFormInvalid"
                @click.prevent="submitForm"
                
            >Create Page</button>
        </div>
    </form>
</template>

<script>
    export default{
        emits: { // Validates the event information. Optional, don't hafve to declare the events
            pageCreated({pageTitle, content, link}) {
                if (!pageTitle){
                    return false;
                }
                if (!content){
                    return false;
                }
                if (!link || !link.text || !link.url){
                    return false;
                }
                return true;
            }
        },
        props: ['pageCreated'],
        computed: {
            isFormInvalid(){
                return !this.pageTitle || !this.content || !this.linkText || !this.linkURL
            }
        },
        data () {
            return {
                pageTitle: "",
                content: "",
                linkText: "",
                linkURL: "",
                published: true,
            }
        },
        methods:{
            submitForm() {
                if (!this.pageTitle || !this.content || !this.linkText || !this.linkURL){
                    alert('Please fill the form.');
                    return;
                }

                // Event to create a page on click
                this.$emit('pageCreated', {
                    pageTitle: this.pageTitle,
                    content: this.content,
                    link: {
                        text: this.linkText,
                        url: this.linkURL
                    },
                    published: this.published
                });

                this.pageTitle ="";
                this.content= "";
                this.linkText="";
                this.linkURL= "";
                this.published =true;
            }
        },
        watch: {
            pageTitle(newTitle, oldTitle) {
                if (this.linkText == oldTitle){
                    this.linkText = newTitle;
                }
            }
        }
    }
</script>