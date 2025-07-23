<template>
  <div class="overflow-x-auto">
    <div class="min-w-max flex justify-center">
      <TreeNode :node="treeData" :depth="0" @show-details="showDetails = $event" />
    </div>

    <NodeDetailsModal v-if="showDetails" :user="showDetails" @close="showDetails = null" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import TreeNode from './components/TreeNode.vue'
import NodeDetailsModal from './components/NodeDetailsModal.vue'
import treeJson from './assets/Daxcsa.json'

const treeData = ref(treeJson.data.attributes[0])
const showDetails = ref(null)
</script>
