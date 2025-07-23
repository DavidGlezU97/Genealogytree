<template>
    <div class="flex flex-col items-center w-full max-w-xs">
        <img src="/src/assets/avatar.png" alt="Avatar" class="w-12 h-12 mb-2 rounded-full border border-gray-300 shadow" />

        <div class="relative bg-white shadow-lg rounded-2xl border border-gray-300 p-4 w-full transition-all hover:shadow-xl hover:scale-105 cursor-pointer text-center"
            :class="{
                'border-l-4 border-green-400': node.binary_placement === 'Left',
                'border-r-4 border-blue-400': node.binary_placement === 'Right'
            }" @click="emit('click')">
            <p class="font-bold text-sm truncate">{{ node.full_name }}</p>
            <p class="text-xs text-gray-500 truncate">{{ node.username }}</p>
            <p v-if="node.product_name || node.category_name" class="text-xs truncate">{{ node.product_name }} ({{
                node.category_name }})</p>

            <p class="text-xs font-semibold flex items-center justify-center gap-1"
                :class="node.status === 'Active' ? 'text-green-600' : 'text-red-500'">
                <CheckCircle v-if="node.status === 'Active'" class="w-4 h-4" />
                <XCircle v-else class="w-4 h-4" />
                {{ node.status }}
            </p>

            <button v-if="node.children?.length" @click.stop="emit('toggle')"
                class="absolute top-2 right-2 text-xs bg-gray-100 hover:bg-gray-200 rounded-full p-1"
                :aria-expanded="expanded" aria-label="Toggle children" title="Toggle Children">
                <ChevronDown v-if="expanded" class="w-4 h-4" />
                <ChevronRight v-else class="w-4 h-4" />
            </button>
        </div>
    </div>
</template>

<script setup>
import { CheckCircle, XCircle, ChevronDown, ChevronRight } from 'lucide-vue-next'

const props = defineProps({
    node: Object,
    expanded: Boolean
})
const emit = defineEmits(['click', 'toggle'])
</script>
