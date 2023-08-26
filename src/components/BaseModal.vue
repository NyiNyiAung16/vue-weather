<template>
<Teleport to="body">
    <Transition name="modal-outer">
    <div class="absolute w-full bg-black bg-opacity-30 h-screen top-0 left-0 flex justify-center px-8"
    v-show="modalActive"
    >
    <Transition name="modal-inner">
        <div v-if="modalActive" class="p-4 bg-white self-start mt-32 max-w-screen-md">
            <slot />
            <button class="text-white mt-8 bg-weather-primary py-2 px-5 border rounded-md" @click="$emit('close-modal')">
                close
            </button>
        </div>
    </Transition>
    </div>
    </Transition>
</Teleport>
</template>

<script setup>
defineProps({
    modalActive:{
        modalActive:Boolean,
        default:false,
    }
})
defineEmits(['close-modal']);
</script>

<style scoped>
.modal-outer-enter-active,
.modal-outer-leave-active{
    transition: opacity 0.3s cubic-bezier(0.52,0.02,0.19,1.02);
}

.modal-outer-enter-from,
.modal-outer-leave-to{
    opacity: 0;
}

.modal-inner-enter-from{
    opacity: 0;
    transform: scale(0.8);
}
.modal-inner-leave-to{
    opacity: 0;
    transform: scale(0.8);
}

.modal-inner-enter-active{
    transition: all 0.3s cubic-bezier(0.52,0.02,0.19,1.02) 0.15s;
}
.modal-inner-leave-active{
    transition: all 0.3s cubic-bezier(0.52,0.02,0.19,1.02) ;
}
</style>