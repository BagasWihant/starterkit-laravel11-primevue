<script setup>
import { ref } from 'vue';
import AppMenuItem from '@/primevue/AppMenuItem.vue';
import { Link } from '@inertiajs/vue3';
import NavLink from '../NavLink.vue';

const submenuShow = ref(true)

const model = ref([
    {
        label: 'Master',
        drop:false,
        child: [
            {
                label: 'Master Barang',
                to: route('barang.index'),
                icon: 'pi pi-fw pi-chart-bar',
                child: null
            },
            {
                label: 'Master Puer',
                to: 'barang',
                icon: 'pi pi-fw pi-chart-bar',
                child: null
            },
        ],
        to: null,
        icon: 'pi pi-fw pi-chart-bar'
    },
    {
        label: 'Dashboard',
        child: null,
        to: route('/'),
        icon: 'pi pi-fw pi-chart-bar'
    },
    {
        label: 'Master',
        drop:false,
        child: [
            {
                label: 'Master Barang',
                to: route('barang.index'),
                icon: 'pi pi-fw pi-chart-bar',
                child: null
            },
            {
                label: 'Master Puer',
                to: 'barang',
                icon: 'pi pi-fw pi-chart-bar',
                child: null
            },
        ],
        to: null,
        icon: 'pi pi-fw pi-chart-bar'
    },
]);

const activeUrl = (url,url1)=>{
    // console.log(url,url1);
    return url.includes(url1) ? 'bg-blue-300' : '';
}

const dropShowOff = (status)=>{
    
    status.drop = status.drop ? false : true
}
</script>


<template>
    <ul class="list-none p-0 m-0 overflow-hidden">
        <li v-for="menu in model">
            <a v-if="menu.child"  @click="dropShowOff(menu)"
                class="flex items-center cursor-pointer p-3 rounded-md text-surface-700 dark:text-surface-0/80 hover:bg-surface-100 dark:hover:bg-surface-700 duration-200 transition-colors">
                <i class="pi pi-chart-line mr-2"></i>
                <span class="font-medium">{{ menu.label }}</span>
                <i class="pi pi-chevron-down ml-auto"></i>
            </a>
            <Link :href="menu.to" v-ripple v-else
                class="flex items-center cursor-pointer p-3 rounded-md text-surface-700 dark:text-surface-0/80 hover:bg-surface-100 dark:hover:bg-surface-700 duration-200 transition-colors "
                :class="activeUrl(menu.to,$page.url)">
                <i class="pi pi-cog mr-2"></i>
                <span class="font-medium">{{ menu.label }}</span>
            </Link>
            {{ menu.drop }}aa
            <ul class="list-none py-0 pl-3 pr-0 m-0 overflow-y-hidden transition-all duration-400 ease-in-out" v-if="menu.drop" :class="[menu.drop ? 'h-auto':'']">
                <li v-for="md in menu.child">
                    <Link v-ripple :href="md.to"
                    :class="activeUrl(md.to,$page.url)"
                        class="flex items-center cursor-pointer p-3 rounded-md text-surface-700 dark:text-surface-0/80 hover:bg-surface-100 dark:hover:bg-surface-700 duration-200 transition-colors">
                        <i class="pi pi-chart-line mr-2"></i>
                        <span class="font-medium">{{ md.label }}</span>
                </Link>
                </li>
            </ul>

        </li>
    </ul>
</template>
