<template>
  <div
    class="flex cursor-pointer whitespace-nowrap items-center justify-center bg-transparent/[0.19] backdrop-brightness-[1.7] hover:backdrop-brightness-[1.9] h-[35px] px-2 rounded space-x-2 transition-[backdrop-brightness]"
  >
    <slot name="leftIcon"></slot>
    <slot></slot>
    <slot name="rightIcon"></slot>
  </div>
</template>
