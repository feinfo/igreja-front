<template>
    <sidebar-menu :menu="menu" />
</template>
<script>
import {SidebarMenu} from 'vue-sidebar-menu'

export default {
    name:'sideBar',
    components:{
        SidebarMenu
    },
    data(){
        return{
             menu: [
                    {
                        header: true,
                        title: 'Menu',
                        hiddenOnCollapse: true
                    },
                    {
                        href: '/',
                        title: 'Dashboard',
                        icon: 'fab fa-medium'
                    },
                    {
                        href: '/charts',
                        title: 'Charts',
                        icon: 'fa fa-chart-area',
                        child: [
                            {
                                href: '/charts/sublink',
                                title: 'Sub Link'
                            }
                        ]
                    }
                ]
        };
    }
}
</script>
<style lang="stylus" scoped>

</style>