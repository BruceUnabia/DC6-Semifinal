<script setup>
    import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
    import { Head, Link, router, useForm } from '@inertiajs/vue3';
    import { inject } from 'vue';
    import Card from '@/Components/Card.vue';


    const props  = defineProps({
        users : Array,
    })

    let deleteForm = useForm({});
    let selectedUserForDelete = null

    function remove(user) {
        selectedUserForDelete = user
        deleteForm.delete('/users/' + selectedUserForDelete.id)

        // console.log(props.errors)
    }
    function edit(){
        router.visit('/clients/edit/' + props.users.id)
    }
    const themeMode = inject('themeMode');
</script>

<template>
    <Head title="User" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl  leading-tight">Users List</h2>
        </template>

        <div class="py-12" :class="themeMode">
            <div class="flex">
                <h1 class="text-3xl font-medium text-gray-700 "></h1>
                <Link style="margin-left:180px" href="users/create"  as="button" class="btn-primary inline-flex items-center mr-20 px-2 py-2 bg-blue-600 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-blue-700 focus:bg-blue-700 active:bg-blue-900 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 transition ease-in-out duration-150">
                    Create User +
                </Link>
            </div>
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class=" overflow-hidden  sm:rounded-lg">
                    <!-- component -->
                    <div class="overflow-hidden rounded-lg border border-gray-200 shadow-md m-5">
                    <table class="w-full border-collapse  text-left text-sm te">
                        <thead class="">
                        <tr>
                            <th scope="col" class="px-6 py-4 font-medium">Id</th>
                            <th scope="col" class="px-6 py-4 font-medium">Name</th>
                            <th scope="col" class="px-6 py-4 font-medium">Email</th>
                            <th scope="col" class="px-6 py-4 font-medium">Action</th>
                        </tr>
                        </thead>
                        <tbody class="divide-y divide-gray-100 border-t border-gray-100" v-for="user in users" :key="user.id">
                        <tr>
                            <th class="flex gap-3 px-6 py-4 font-normal ">

                            <div class="text-sm">
                                <div class="font-medium ">{{ user.id }}</div>

                            </div>
                            </th>
                            <td class="px-6 py-4">{{ user.name }}</td>
                            <td class="px-6 py-4">  {{ user.email }}</td>



                            <td class="px-6 py-4">
                            <div class="flex justify-start gap-4">
                                <button style="color:red;" @click="remove(user)" x-data="{ tooltip: 'Delete' }" href="#">
                                Delete
                                </button>
                                <Link style="color:green;" x-data="{ tooltip: 'Edite' }" :href="'/users/edit/'+user.id">
                                Update
                                </Link>
                            </div>
                            </td>
                        </tr>

                        </tbody>
                    </table>
                    </div>
                </div>
            </div>
        </div>
        <div class="grid">

            <Card v-for="usr in users" :key="usr.id">

                <template v-slot:head>


                    <div class="relative flex h-32 w-full justify-center rounded-xl bg-cover mt-2" >
                                    <!-- <img src='https://horizon-tailwind-react-git-tailwind-components-horizon-ui.vercel.app/static/media/banner.ef572d78f29b0fee0a09.png' class="absolute flex h-32 w-full justify-center rounded-xl bg-cover"> -->
                                    <div class="absolute  flex h-[87px] w-[87px] items-center justify-center rounded-full border-[4px] border-white bg-pink-400 dark:!border-navy-700">
                                        <img class="h-full w-full rounded-full" src="https://i.pinimg.com/564x/73/d1/09/73d10901ec00f102b2274dc7b72857cc.jpg" alt="" />
                                    </div>
                    </div>


                </template>

                <template v-slot:content>
                    <div class="text-center">
                        <h5 class="mb-1 text-xl font-medium text-gray-900 dark:text-dark">{{usr.name}}</h5>
                        <span class="text-sm text-gray-500 dark:text-gray-400">{{usr.email}}</span>
                    </div>

                </template>

                <template v-slot:footer>

                    <div class="flex mt-4 space-x-3 md:mt-6 justify-center">
                        <a href="#" class="inline-flex items-center px-4 py-2 text-sm font-medium text-center text-white bg-green-700 rounded-lg hover:bg-green-800 focus:ring-4 focus:outline-none dark:bg-green-500 dark:hover:bg-green-600 dark:focus:ring-green-800">Update</a>
                        <a href="#" class="inline-flex items-center px-4 py-2 text-sm font-medium text-center text-white bg-red-700 rounded-lg hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-red-300 dark:bg-pink-600 dark:hover:bg-pink-700 dark:focus:ring-pink-800">Delete</a>
                    </div>


                </template>

            </Card>

        </div>
    </AuthenticatedLayout>

</template>

<style scoped>

.grid{
    display: grid;
    grid-template-columns: repeat(3, 1fr) ;
    gap: 25px 24px;
}
</style>
