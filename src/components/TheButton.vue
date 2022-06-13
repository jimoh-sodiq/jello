<template>
  <div
    class="flex cursor-pointer whitespace-nowrap items-center justify-center bg-[#6FCC89] h-[35px] px-2 rounded space-x-2 hover:brightness-105 transition-[brightness]"
  >
    <slot name="leftIcon"></slot>
    <slot></slot>
    <slot name="rightIcon"></slot>
  </div>
</template>
