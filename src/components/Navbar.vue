<template>
    <nav 
        :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
    >
        <div class="container-fluid">
        <a class="navbar-brand" href="#">My Vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <navbar-link
                    v-for="(page, index) in publishedPages" class="nav-item" :key="index"
                    :page="page"
                    :index="index"

                ></navbar-link>

                <li>
                    <router-link
                        to="/create"
                        class="nav-link"
                        active-class="active"
                        aria-current="page"
                    >Create Page</router-link>
                </li>
            </ul>
            <form class="d-flex">
                <button 
                    class="btn btn-primary" 
                    @click.prevent="changeTheme()">
                Toggle Nav Bar</button>
            </form>
        </div>
    </nav>
</template>

<script>
    import NavbarLink from './NavbarLink.vue';


    export default{
        components: {
            NavbarLink
        },
        created() {
            this.getThemeSettings();
            this.pages = this.$pages.getAllPages();
        },
        props: ['pages'], // Props are read-only
        computed: {
            publishedPages() {
               return this.pages.filter(p => p.published)
            }
        },
        data() {
            return {
                theme: 'dark',
                data: []
            }
        }, 
        methods:{
            changeTheme() {
                let theme = 'light';

                if (this.theme == 'light'){
                    theme = 'dark';
                }

                this.theme = theme;
                this.storeThemeSettings();
            },
            storeThemeSettings() {
                localStorage.setItem('theme', this.theme);
            }, 
            getThemeSettings() {
                let theme = localStorage.getItem('theme', this.theme);

                if (theme) {
                    this.theme = theme;
                }
            }
        }
    }
</script>