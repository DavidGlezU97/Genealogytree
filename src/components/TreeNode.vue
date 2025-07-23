<template>
  <div class="relative flex flex-col items-center">
    <TreeNodeCard :node="node" :expanded="expanded" @toggle="expanded = !expanded" @click="openDetails" />

    <div v-if="node.children?.length" class="h-4 w-0.5 bg-gray-400"></div>

    <transition name="fade">
      <div v-if="expanded && node.children?.length" class="flex flex-wrap justify-center gap-4 mt-2 relative w-full">
        <svg class="absolute top-0 left-0 w-full h-4" viewBox="0 0 100 10" preserveAspectRatio="none">
          <line x1="10" y1="0" x2="90" y2="0" stroke="gray" stroke-width="1" />
        </svg>

        <template v-for="child in sortedChildren" :key="child.distributor_id">
          <div class="flex flex-col items-center">
            <div class="w-0.5 h-4 bg-gray-400"></div>
            <TreeNode :node="child" :depth="depth + 1" @show-details="emit('show-details', $event)" />
          </div>
        </template>
      </div>
    </transition>
  </div>
</template>
  
<script setup>
import { ref, computed } from 'vue'
import TreeNodeCard from './TreeNodeCard.vue'

const props = defineProps({
  node: { type: Object, required: true },
  depth: { type: Number, default: 0 }
})

const emit = defineEmits(['show-details'])

const expanded = ref(props.depth < (window.innerWidth < 640 ? 1 : 2))

const sortedChildren = computed(() =>
  [...(props.node.children || [])].sort((a, b) =>
    a.binary_placement === 'Left' ? -1 : 1
  )
)

const openDetails = () => {
  emit('show-details', props.node)
}
</script>
  