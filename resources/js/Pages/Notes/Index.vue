<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Note from '@/Components/Notes/Note.vue';
import InputError from '@/Components/InputError.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { useForm, Head } from '@inertiajs/vue3';

defineProps(['notes']);

const form = useForm({
    content: '',
});
</script>

<template>
    <Head title="Notes" />

    <AuthenticatedLayout>
        <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
            <form @submit.prevent="form.post(route('notes.store'), { onSuccess: () => form.reset() })">
                <textarea
                    v-model="form.content"
                    placeholder="What's on your mind?"
                    class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
                ></textarea>
                <InputError :content="form.errors.content" class="mt-2" />
                <PrimaryButton class="mt-4">Note</PrimaryButton>
            </form>

            <div class="mt-6 bg-white shadow-sm rounded-lg divide-y">
                <Note
                    v-for="note in notes"
                    :key="note.id"
                    :note="note"
                />
            </div>

        </div>
    </AuthenticatedLayout>
</template>