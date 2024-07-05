<script setup>
import Navbar from '@/components/Navbar.vue';
import Sidebar from '@/components/Sidebar.vue';
import Table from '@/components/Table.vue';

</script>

<template>
    <Navbar />
    <Sidebar />
      
      <!-- body  -->
      <div class="p-4 sm:ml-64">
         <div class="p-4 border-2 border-gray-200 border-dashed rounded-lg dark:border-gray-700 mt-14">
             <RouterView />
         </div>
      </div>
</template>