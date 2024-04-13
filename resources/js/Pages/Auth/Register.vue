<template>
    <Head title="Register" />
    <div class="flex flex-row justify-center items-center min-h-screen">
        <Card class="mx-auto max-w-sm sm:w-96">
            <CardHeader>
                <CardTitle class="text-xl">
                    Sign Up
                </CardTitle>
                <CardDescription>
                    Enter your information to create an account
                </CardDescription>
            </CardHeader>
            <CardContent>
                <div class="grid gap-4">
                    <div class="grid gap-2">
                        <FormGroupInput
                            v-model="form.name"
                            id="name" label="Name"
                            type="text" placeholder=""
                            :required="true" :error="form.errors.name"
                        />
                    </div>
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
                    <div class="grid gap-2">
                        <FormGroupInput
                            v-model="form.password_confirmation"
                            id="password_confirmation" label="Confirm Password"
                            type="password" placeholder=""
                            :required="true" :error="form.errors.password_confirmation"
                        />
                    </div>
                    <Button 
                        @click="submit()"
                        type="submit" class="w-full"
                        :class="[form.processing && 'cursor-progress']"
                    >
                        Create an account
                    </Button>
                    <Button variant="outline" class="w-full cursor-not-allowed">
                        Sign up with Google
                    </Button>
                </div>
                <div class="mt-4 text-center text-sm">
                    Already have an account?
                    <Link :href="route('login')" class="underline">
                        Sign in
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

const mode = useColorMode();

const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});

const submit = () => {
    form.post(route('register'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>
