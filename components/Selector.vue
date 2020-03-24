<template>
  <button class="button rounded-full mx-1 my-1" @click="$emit('switch')">
    <slot />
  </button>
</template>

<script>
export default {

}
</script>
