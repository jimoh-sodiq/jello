<script setup>
const emit = defineEmits(["closeModal"]);
</script>

<template>
  <teleport to="body">
    <div
      class="w-full h-full z-50 flex items-center min-h-fit justify-center fixed top-0 left-0 overflow-y-scroll pt-[300px] px-2 bg-transparent/50"
      @click.self="emit('closeModal')"
    >
      <div
        class="bg-[#F4F5F7] w-full relative rounded-sm max-w-[850px] h-auto pb-8 mb-12 mt-[100px] md:mt-0"
      >
        <slot></slot>
      </div>
    </div>
  </teleport>
</template>
