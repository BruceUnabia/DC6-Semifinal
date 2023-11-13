<script setup>
    import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
    import { Head, Link, router, useForm } from '@inertiajs/vue3';
    import { inject } from 'vue';
    import Card from'@/Components/Card.vue';

    const props  = defineProps({
        products : Object
    })

    let deleteForm = useForm({});
    let selectedProductForDelete = null

    function remove(prod) {
        selectedProductForDelete = prod
        deleteForm.delete('/products/' + selectedProductForDelete.id)

        // console.log(props.errors)
    }


    const themeMode = inject('themeMode');

</script>

<template>
    <Head title="Product" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl leading-tight">Product List</h2>
        </template>

        <div class="py-2">
                <div style="margin-left: 170px">
                <h1 class="text-3xl font-medium text-gray-700"></h1>
                <Link href="products/create" as="button" class="items-center mr-20 px-2 py-2 bg-blue-600 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest focus:bg-blue-700 active:bg-blue-900 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 transition ease-in-out duration-150">
                    Create Product +
                </Link>
                </div>
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="" :class="themeMode">
                    <div class="m-5" v-for="prod in products" :key="prod.id">
                        <div class="overflow-hidden rounded-lg border border-gray-200 shadow-md mb-5">
                            <div class="px-6 py-4">
                                <h3 class="text-xl font-semibold">{{ prod.name }}</h3>
                                <p class="text-gray-700">{{ prod.description }}</p>
                            </div>
                            <div class="px-6 py-4">
                                <div class="flex items-center">
                                    <p class="text-sm font-medium text-gray-700">Retail Price:</p>
                                    <p class="ml-2 text-sm text-gray-600">{{ prod.retail_price }}</p>
                                </div>
                                <div class="flex items-center">
                                    <p class="text-sm font-medium text-gray-700">Stock Qty:</p>
                                    <p class="ml-2 text-sm text-gray-600">{{ prod.qty_stock }}</p>
                                </div>
                                <div class="flex items-center">
                                    <p class="text-sm font-medium text-gray-700">Category:</p>
                                    <p class="ml-2 text-sm text-gray-600">{{ prod.category.name }}</p>
                                </div>
                            </div>
                            <div class="px-6 py-4">
                                <div class="flex justify-start gap-4">
                                    <button style="color:red;" @click="remove(prod)" x-data="{ tooltip: 'Delete' }" href="#">
                                        Delete
                                    </button>
                                    <Link style="color:green;" x-data="{ tooltip: 'Edit' }" :href="'/products/edit/' + prod.id">
                                        Update
                                    </Link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="justify-between">

<Card>

    <template v-slot:head>


        <div class="flex h-100 justify-center rounded-xl bg-cover" >
            <div class="w-full p-4 text-center bg-white border border-gray-200 rounded-lg shadow sm:p-8">
                <h5 class="mb-2 text-3xl font-bold text-gray-900 dark:text-white">To view more products click button below</h5>
            </div>
        </div>


        </template>

        <template v-slot:content>

        </template>

        <template v-slot:footer>

        <div class="flex mt-4 space-x-3 md:mt-6 justify-center">
            <div class="items-center justify-center space-y-4 sm:flex sm:space-y-0 sm:space-x-4">
                <a href="#" class="w-full sm:w-auto bg-gray-800 hover:bg-gray-700 focus:ring-4 focus:outline-none focus:ring-gray-300 text-white rounded-lg inline-flex items-center justify-center px-4 py-2.5 dark:bg-gray-700 dark:hover:bg-gray-600 dark:focus:ring-gray-700">
                    <div class="text-left">
                        <div class="mb-1 text-xs">Click here..</div>
                    </div>
                </a>
            </div>
        </div>


    </template>



</Card>



</div>
    </AuthenticatedLayout>
</template>
