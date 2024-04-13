<template>
    <Head :title="props.title" />
    <div>
        <!-- Header -->
        <div
            class="fixed top-0 left-0 right-0 supports-backdrop-blur:bg-background/60 border-b bg-background/95 backdrop-blur z-20">
            <nav class="h-14 flex items-center justify-between px-4">
                <div class="hidden lg:block">
                    <Link href="/">
                        <!--Logo-->
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" class="mr-2 h-6 w-6">
                            <path d="M15 6v12a3 3 0 1 0 3-3H6a3 3 0 1 0 3 3V6a3 3 0 1 0-3 3h12a3 3 0 1 0-3-3" />
                        </svg>
                    </Link>
                </div>
                <div class="block lg:!hidden">
                    <!--Mobile Sidebar-->
                    <Sheet>
                        <SheetTrigger>
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"
                                fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                stroke-linejoin="round" class="lucide lucide-menu" type="button" aria-haspopup="dialog"
                                aria-expanded="false" aria-controls="radix-:R4rrqla:" data-state="closed">
                                <line x1="4" x2="20" y1="12" y2="12"></line>
                                <line x1="4" x2="20" y1="6" y2="6"></line>
                                <line x1="4" x2="20" y1="18" y2="18"></line>
                            </svg>
                        </SheetTrigger>
                        <SheetContent side="left" class="!px-0">
                            <div class="space-y-4 py-4">
                                <div class="px-3 py-2">
                                    <h2 class="mb-2 px-4 text-lg font-semibold tracking-tight">
                                        Overview
                                    </h2>
                                    <div class="space-y-1">
                                        <!-- Side Navigation Here -->
                                        <SideNavigation />
                                    </div>
                                </div>
                            </div>
                        </SheetContent>
                    </Sheet>
                </div>

                <div class="flex items-center gap-2">
                    <Header :user="user" />
                </div>
            </nav>
        </div>

        <!-- Page Content -->
        <div class="flex h-screen overflow-hidden">
            <!--Dasktop Sidebar-->
            <nav class="relative hidden h-screen border-r pt-16 lg:block w-72">
                <div class="space-y-4 py-4">
                    <div class="px-3 py-2">
                        <div class="space-y-1">
                            <h2 class="mb-2 px-4 text-xl font-semibold tracking-tight">
                                Overview
                            </h2>
                            <SideNavigation />
                        </div>
                    </div>
                </div>
            </nav>
            <!--Main Section-->
            <main class="w-full pt-16">
                <slot />
            </main>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue'
import { Link, Head, usePage } from '@inertiajs/vue3';

import { Sheet, SheetContent, SheetTrigger } from "@/Components/ui/sheet";

import Header from '@/Layouts/Header.vue';
import SideNavigation from '@/Layouts/SideNavigation.vue';

const props = defineProps({
    title: String,
})

const page = usePage()
const user = computed(() => page.props.auth.user)
</script>
