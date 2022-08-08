<!--
    - <ToggleSwitch v-model:toggle="<Boolean Value>" />
-->

<template>
    <div
        :class="['container', toggle ? 'bg-green-50' : 'bg-gray-40']"
        @click="() => $emit('update:toggle', !toggle)"
    >
        <div :class="['child', toggle ? 'on' : 'off']"></div>
    </div>
</template>

<script setup>
defineProps({
    toggle: {
        type: Boolean,
        default: false,
    },
});

defineEmits(["update:toggle"]);
</script>

<style lang="scss" scoped>
.container {
    width: 2.375rem;
    @apply flex items-center h-5 relative cursor-pointer rounded-2xl;
}
.child {
    @apply bg-white rounded-full absolute h-4 w-4 transform duration-150 ease-linear;
}
.on {
    left: 52.63%;
    right: 5.26%;
}
.off {
    right: 52.63%;
    left: 5.26%;
}
</style>
