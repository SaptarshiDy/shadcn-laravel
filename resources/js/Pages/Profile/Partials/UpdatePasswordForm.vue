<script setup>
import { Button } from '@/Components/ui/button';
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/Components/ui/card';

import FormGroupInput from '@/Components/Form/FormGroupInput.vue'

import { useForm } from '@inertiajs/vue3';
import { ref } from 'vue';

const passwordInput = ref(null);
const currentPasswordInput = ref(null);

const form = useForm({
    current_password: '',
    password: '',
    password_confirmation: '',
});

const updatePassword = () => {
    form.put(route('password.update'), {
        preserveScroll: true,
        onSuccess: () => form.reset(),
        onError: () => {
            if (form.errors.password) {
                form.reset('password', 'password_confirmation');
                passwordInput.value.focus();
            }
            if (form.errors.current_password) {
                form.reset('current_password');
                currentPasswordInput.value.focus();
            }
        },
    });
};
</script>

<template>
    <Card>
        <CardHeader>
            <CardTitle>
                <h2 class="text-lg font-medium text-gray-900 dark:text-gray-100">Update Password</h2>

                <p class="mt-1 text-sm text-gray-600 dark:text-gray-400">
                    Ensure your account is using a long, random password to stay secure.
                </p>
            </CardTitle>
        </CardHeader>

        <CardContent>
            <form @submit.prevent="updatePassword" class="mt-6 space-y-6">
                <div>
                    <FormGroupInput
                        v-model="form.current_password"
                        id="current_password" label="Current Password"
                        type="password" placeholder=""
                        :required="true" :error="form.errors.current_password"
                    />
                </div>

                <div>
                    <FormGroupInput
                        v-model="form.password"
                        id="password" label="New Password"
                        type="password" placeholder=""
                        :required="true" :error="form.errors.password"
                    />
                </div>

                <div>
                    <FormGroupInput
                        v-model="form.password_confirmation"
                        id="password_confirmation" label="Confirm Password"
                        type="password" placeholder=""
                        :required="true" :error="form.errors.password_confirmation"
                    />
                </div>

                <div class="flex items-center gap-4">
                    <Button :disabled="form.processing">Save</Button>

                    <Transition
                        enter-active-class="transition ease-in-out"
                        enter-from-class="opacity-0"
                        leave-active-class="transition ease-in-out"
                        leave-to-class="opacity-0"
                    >
                        <p v-if="form.recentlySuccessful" class="text-sm text-gray-600 dark:text-gray-400">Saved.</p>
                    </Transition>
                </div>
            </form>
        </CardContent>
    </Card>
</template>
