<template>
    <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50" @click.self="$emit('close')">
        <div
            class="bg-white rounded-xl p-6 shadow-2xl w-[90%] max-w-md text-sm space-y-2 max-h-[90vh] overflow-y-auto relative">
            <button class="absolute top-2 right-2 text-gray-500" @click="$emit('close')" aria-label="Close modal">
                <X class="w-5 h-5" />
            </button>
            <h2 class="text-xl font-semibold">{{ user.full_name }}</h2>
            <div class="border-t pt-2 space-y-1">
                <p><strong>User ID:</strong> {{ user.distributor_id }}</p>
                <p><strong>Username:</strong> {{ user.username }}</p>
                <p>
                    <strong>Status: </strong>
                    <span :class="user.status === 'Active' ? 'text-green-600' : 'text-red-500'">
                        <CheckCircle v-if="user.status === 'Active'" class="w-4 h-4 inline" />
                        <XCircle v-else class="w-4 h-4 inline" />
                        {{ user.status }}
                    </span>
                </p>
                <p><strong>Product:</strong> {{ user.product_name }}</p>
                <p><strong>Category:</strong> {{ user.category_name }}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
import { X, CheckCircle, XCircle } from 'lucide-vue-next'
defineProps({ user: Object })
</script>
