<script setup>
</script>

<template>
    <!-- Eye symbol -->
    <svg 
        @click="$emit('togglePasswordVisibility')"
        class="toggle_password"
        width="24px" height="24px" 
        viewBox="0 0 24 24" 
        fill="none" 
        xmlns="http://www.w3.org/2000/svg">
            <path 
                d="M1 12C1 12 5 4 12 4C19 4 23 12 23 12" 
                stroke="rgb(98, 116, 139)" 
                stroke-width="2" 
                stroke-linecap="round" 
                stroke-linejoin="round"/>
            <path 
                d="M1 12C1 12 5 20 12 20C19 20 23 12 23 12" 
                stroke="rgb(98, 116, 139)" 
                stroke-width="2" 
                stroke-linecap="round" 
                stroke-linejoin="round"/>
            <circle 
                cx="12" cy="12" r="3" 
                stroke="rgb(98, 116, 139)" 
                stroke-width="2" 
                stroke-linecap="round" 
                stroke-linejoin="round"/>
    </svg>
</template>

<style scoped>
    /* This style should be shared with ShowPasswordSymbol.vue */
    .toggle_password {
        cursor: pointer;
    }
</style>