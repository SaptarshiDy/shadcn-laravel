<template>
    <nav className="grid items-start gap-2">
        <Link
            v-for="(item, index) in items" :key="index"
            :href="item.href"
        >
            <span
                class="group flex items-center rounded-md px-3 py-2 text-sm font-medium hover:bg-accent hover:text-accent-foreground"
                :class="[
                    item.active ? 'bg-accent' : 'transparent',
                    item.disabled && 'cursor-not-allowed opacity-80',
                ]"
            >
                <Icon :icon="item.icon" class="mr-2 h-4 w-4" />
                <span>{{ item.title }}</span>
            </span>
        </Link>
    </nav>
</template>

<script setup>
import { ref } from 'vue';
import { Link } from '@inertiajs/vue3';
import { Icon } from '@iconify/vue'

const items = [
    {
        title: "Dashboard",
        href: "/dashboard",
        icon: "radix-icons:dashboard",
        active: route().current('dashboard'),
        disabled: false,
    },
    {
        title: "User",
        href: "/dashboard/user",
        icon: "radix-icons:person",
        active: false,
        disabled: false,
    },
    {
        title: "Employee",
        href: "/dashboard/employee",
        icon: "radix-icons:dashboard",
        active: false,
        disabled: false,
    },
    {
        title: "Profile",
        href: "/dashboard/profile",
        icon: "radix-icons:avatar",
        active: false,
        disabled: false,
    },
    {
        title: "Kanban",
        href: "/dashboard/kanban",
        icon: "radix-icons:dashboard",
        active: false,
        disabled: false,
    },
    {
        title: "Logout",
        href: "/logout",
        icon: "radix-icons:dashboard",
        active: false,
        disabled: false,
    },
]
</script>