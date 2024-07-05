<script setup>
    import { reactive, onMounted } from 'vue';
    import axios from 'axios';
    import router from '@/router';
    import { useToast } from 'vue-toastification';

    
    const toast = useToast();
    const loginForm = reactive({
        username: '',
        password: '',
    });

    const handleSubmit = async () => {
        const login = {
            username: loginForm.username,
            password: loginForm.password
        }
        console.log(login)
        try {
        const response = await axios.post(`${import.meta.env.VITE_API_KEY}/login`, login);
            // to do toast
            console.log(response.data.message)
            toast.success(response.data.message);
            router.push(`/dashboard`);
        } catch (error) {
            console.log(error.response.data.errors.message)
            toast.error(error.response.data.errors.message[0]);
        }
    };


</script>


<template>
    <section class="bg-gray-50 dark:bg-gray-900">
        <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
            <a href="#" class="flex items-center mb-6 text-2xl font-semibold text-gray-900 dark:text-white">
                <img class="w-8 h-8 mr-2" src="https://flowbite.s3.amazonaws.com/blocks/marketing-ui/logo.svg" alt="logo">
                   
            </a>
            <div class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
                <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
                    <h1 class="text-center text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white">
                        Login
                    </h1>
                    <form class="space-y-4 md:space-y-6" action="#"  @submit.prevent="handleSubmit">
                        <div>
                            <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your username</label>
                            <input v-model="loginForm.username" type="text" name="username" id="text" class="bg-gray-50 border border-gray-300 text-gray-900 rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="username" required="">
                        </div>
                        <div>
                            <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
                            <input v-model="loginForm.password" type="password" name="password" id="password" placeholder="••••••••" class="bg-gray-50 border border-gray-300 text-gray-900 rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required="">
                        </div>
                        <div class="flex items-center justify-between">
                            <div class="flex items-start">
                            </div>
                            <a href="#" class="text-sm font-medium text-primary-600 hover:underline dark:text-primary-500">Forgot password?</a>
                        </div>
                        <button type="submit" style="background-color: #15803d;" class="w-full text-black hover:bg-green-800 focus:ring-4 focus:outline-none focus:ring-green-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:hover:bg-green-700 dark:focus:ring-green-800">
                            Login
                        </button>                        
                        <!-- <p class="text-sm font-light text-gray-500 dark:text-gray-400">
                            Don’t have an account yet? <a href="#" class="font-medium text-primary-600 hover:underline dark:text-primary-500">Sign up</a>
                        </p> -->
                    </form>
                </div>
            </div>
        </div>
      </section>
</template>