<script setup>
const emit = defineEmits(["closeModal"]);
</script>

<template>
  <teleport to="body">
    <div
      class="w-full h-full z-50 flex items-center justify-center fixed top-0 left-0 overflow-y-scroll px-2 pb-8 pt-[130px] bg-transparent/50"
      @click.self="emit('closeModal')"
    >
      <div
        class="bg-[#F4F5F7] w-full relative rounded-sm max-w-[850px] h-auto min-h-screen"
      >
        <slot></slot>
      </div>
    </div>
  </teleport>
</template>
