<script setup>
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';
defineProps({
    categories: {
        type: Array
    }
})
const form = useForm({
    name: '',
    email: '',
    phone: '',
    address: '',
    category: '',
});
const submit = () => {
    form.post(route('contact.store'))
};
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">Create Contacts</h2>
        </template>
        <div class="py-12">
            <div class="max-w-3xl  py-12 mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="relative py-12 overflow-x-auto shadow-md sm:rounded-lg">
                        <form @submit.prevent="submit" class="max-w-md mx-auto">
                            <h2 class="text-center py-4 text-lg">Create Contact</h2>
                            <div>
                                <InputLabel for="name" value="Contact Name" />

                                <TextInput id="name" type="text" class="mb-4 block w-full" v-model="form.name" autofocus />

                                <InputError class="mt-2" :message="form.errors.name" />
                            </div>
                            <div>
                                <InputLabel for="email" value="Contact email" />

                                <TextInput id="email" type="email" class="mb-4 block w-full" v-model="form.email" />

                                <InputError class="mt-2" :message="form.errors.email" />
                            </div>
                            <div>
                                <InputLabel for="phone" value="Contact phone" />

                                <TextInput id="phone" type="tel" class="mb-4 block w-full" v-model="form.phone" />

                                <InputError class="mt-2" :message="form.errors.phone" />
                            </div>
                            <div>
                                <InputLabel for="address" value="Contact address" />

                                <TextInput id="address" type="text" class="mb-4 block w-full" v-model="form.address" />

                                <InputError class="mt-2" :message="form.errors.address" />
                            </div>
                            <div class="mb-4">
                                <label class="block text-gray-700 text-sm font-bold mb-2" for="category">
                                    Category
                                </label>
                                <select
                                    class="appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                    id="category" v-model="form.category">
                                    <option value="">Select a category</option>
                                    <option v-for="category in categories" :key="category.id" :value="category.id">
                                        {{ category.name }}
                                    </option>
                                </select>
                                <InputError class="mt-2" :message="form.errors.category" />

                            </div>
                            <div class="flex items-center justify-center">
                                <Link :href="route('categories')"
                                    class="font-medium  text-blue-600 dark:text-blue-500 hover:underline mx-1">Cancel
                                </Link>
                                <PrimaryButton class="w-42 ml-4 my-3" :class="{ 'opacity-25': form.processing }"
                                    :disabled="form.processing">
                                    Submit
                                </PrimaryButton>
                            </div>
                        </form>

                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
