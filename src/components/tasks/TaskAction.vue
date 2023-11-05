<template>
    <div class="task-actions">
        <button
        class="btn btn-sm btn-circle btn-outline-secondary me-1"
        @click="$event => emit('edit')">
        <IconPen />
        </button>                  
        <button class="btn btn-sm btn-circle btn-outline-danger"
         @click="$event => emit('remove')">
        <IconTrash />
        </button>
    </div>
</template>
<script setup>
import IconPen from "../icons/IconPen.vue";
import IconTrash from "../icons/IconTrash.vue";

const emit = defineEmits(['edit', 'remove'])

</script>