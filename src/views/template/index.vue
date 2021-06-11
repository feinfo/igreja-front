<template>
    <b-container>
        <sidebar-menu :menu="menu" :width="width" @toggle-collapse="onToggleCollapse"/>
    </b-container>
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
                    },
                    {
                        href: '/',
                        title: 'Dashboard',
                        icon: 'fa fa-chart-bar'
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
                    },
                    
                ],
                width: '150px',
        };
    },
    methods: {
    onToggleCollapse(collapsed) {
        //console.log("escondendo" + collapsed)
        this.$emit('collapsed', collapsed);
    },
    //onItemClick(event, item) {}
}
}
</script>
<style scoped>

</style>