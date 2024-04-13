<template>
    <Head title="Login" />
    <div class="flex flex-row justify-center items-center min-h-screen">
        <Card class="mx-auto max-w-sm sm:w-96">
            <CardHeader>
                <CardTitle class="text-xl">
                    Sign In
                </CardTitle>
                <CardDescription>
                    Enter your email below to login to your account
                </CardDescription>
            </CardHeader>
            <CardContent>
                <div class="grid gap-4">
                    <div class="grid gap-2">
                        <FormGroupInput
                            v-model="form.email"
                            id="email" label="Email"
                            type="email" placeholder=""
                            :required="true" :error="form.errors.email"
                        />
                    </div>
                    <div class="grid gap-2">
                        <FormGroupInput
                            v-model="form.password"
                            id="password" label="Password"
                            type="password" placeholder=""
                            :required="true" :error="form.errors.password"
                        />
                    </div>
                    <Button 
                        @click="submit()"
                        type="submit" class="w-full"
                        :class="[form.processing && 'cursor-progress']"
                    >
                        Login
                    </Button>
                    <Button variant="outline" class="w-full cursor-not-allowed">
                        Sign in with Google
                    </Button>
                </div>
                <div class="mt-4 text-center text-sm">
                    Don't have an account?
                    <Link :href="route('register')" class="underline">
                        Sign up
                    </Link>
                </div>
            </CardContent>
        </Card>
    </div>
</template>

<script setup>
import { useColorMode } from '@vueuse/core'
import { Head, Link, useForm } from '@inertiajs/vue3';

import { Button } from '@/Components/ui/button';
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/Components/ui/card';

import FormGroupInput from '@/Components/Form/FormGroupInput.vue'

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const mode = useColorMode();

const form = useForm({
    email: '',
    password: '',
    remember: true,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>
