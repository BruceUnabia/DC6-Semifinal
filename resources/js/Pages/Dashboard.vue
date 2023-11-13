<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { inject } from 'vue';
import Card from '@/Components/Card.vue';

const themeMode = inject('themeMode');
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl leading-tight">Dashboard</h2>
        </template>

        <div class="py-12" :class="themeMode">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class=" overflow-hidden shadow-sm sm:rounded-lg">
                    <Card>

                        <template v-slot:head>


                            <div class="relative flex h-50 w-50 justify-center" >
                                <img src="https://blog.smart.com.ph/wp-content/uploads/2023/05/S23-Redefines-the-Premium-Experience.jpg?w=1170" alt="Sunset in the mountains">
                            </div>


                            </template>

                            <template v-slot:content>
                            <div class="text-center">
                                <div class="px-6 py-4">
                                    <div class="font-bold text-xl mb-2">Latest Product</div>
                                    <p class="text-white text-base">
                                        Samsung S23 Ultra
                                    </p>
                                </div>
                            </div>

                            </template>

                            <template v-slot:footer>

                            <div class="flex mt-4 space-x-3 md:mt-6 justify-center">
                                <div class="px-6 pt-4 pb-2">
                                    <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">Click for more</span>
                                </div>
                            </div>


                        </template>



                    </Card>


                </div>


            </div>
        </div>


    </AuthenticatedLayout>
</template>
