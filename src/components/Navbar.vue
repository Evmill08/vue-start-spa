<template>
    <nav 
        :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
    >
        <div class="container-fluid">
        <a class="navbar-brand" href="#">My Vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <li v-for="(page, index) in pages" class="nav-item" :key="index"> <!--v-for loops through each link in links, links has to be defined in mounted Vue instance-->
                    <navbar-link
                        :page="page"
                        :isActice = "activePage==index"
                        @click.prevent="navLinkClick(index)"
                    ></navbar-link>
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
        props: ['pages', 'activePage', 'navLinkClick'], // Props are read-only
                
        data() {
            return {
                theme: 'dark',
            }
        }, 
        methods:{
            changeTheme() {
                let theme = 'light';

                if (this.theme == 'light'){
                    theme = 'dark';
                }

                this.theme = theme;
            }
        }
    }
</script>