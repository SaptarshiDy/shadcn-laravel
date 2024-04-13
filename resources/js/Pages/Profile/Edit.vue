<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import DeleteUserForm from './Partials/DeleteUserForm.vue';
import UpdatePasswordForm from './Partials/UpdatePasswordForm.vue';
import UpdateProfileInformationForm from './Partials/UpdateProfileInformationForm.vue';

import { ScrollArea } from '@/Components/ui/scroll-area'


defineProps({
    mustVerifyEmail: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});
</script>

<template>
    <Head title="Profile" />

    <AuthenticatedLayout title="profile">
        <ScrollArea className="h-full">
            <div class="flex-1 space-y-4 p-4 md:p-8 pt-6">
                <UpdateProfileInformationForm
                    :must-verify-email="mustVerifyEmail"
                    :status="status"
                    class="max-w-xl"
                />
                <UpdatePasswordForm class="max-w-xl"/>
                <DeleteUserForm class="max-w-xl" />
            </div>
        </ScrollArea>
    </AuthenticatedLayout>
</template>
