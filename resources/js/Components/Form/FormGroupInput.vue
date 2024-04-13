<template>
    <Label v-if="props.label" :for="props.id">{{ props.label }}</Label>
    <Input 
        :id="props.id" :type="props.type" v-model="modelValue"
        :placeholder="props.placeholder" :required="props.required" :autocomplete="autocomplete"
        class="mt-1 placeholder:text-neutral-400 dark:placeholder-text-neutral-600 focus-visible:ring-1 focus-visible:ring-neutral-400 dark:focus-visible:ring-neutral-600 autofill:bg-gray-400"
        :class="[props.error && 'ring-1 ring-red-400']"
    />
    <p class="mt-1 text-sm text-red-600 dark:text-red-400">{{ props.error }}</p>
</template>

<script setup>
import { useVModel } from "@vueuse/core";
import { Input } from '@/Components/ui/input';
import { Label } from '@/Components/ui/label';

const props = defineProps({
    id: String,
    label: String,
    required: {
        type: Boolean,
        default: false,
    },
    defaultValue: { 
        type: [String, Number],
        required: false 
    },
    modelValue: { 
        type: [String, Number],
        required: false
    },
    class: { 
        type: null,
        required: false
    },
    type: {
        type: String,
        default: 'text'
    },
    disabled: {
        type: Boolean,
        default: false
    },
    error: String,
    placeholder: String,
    autocomplete: {
        type: String,
        default: 'off'
    },
});

const emits = defineEmits(["update:modelValue"]);

const modelValue = useVModel(props, "modelValue", emits, {
    passive: true,
    defaultValue: props.defaultValue,
});
</script>