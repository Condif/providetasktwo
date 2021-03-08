<template>
  <button :style="styles"  @click="$emit('add')">
    <slot></slot>
  </button>
</template>

<script>
export default {
    props: {
        border: {default: "none"},
        color: {default: "white"},
        padding: {default: "1rem"},
        borderRadius: {default: "1rem"},
        background: {default: "rgb(109,216,83)"},
        cursor: {default: "pointer"},
    },
    computed: {
        styles() {
            return {
                border: this.border,
                color: this.color,
                padding: this.padding,
                borderRadius: this.borderRadius,
                background: this.background,
                cursor: this.cursor,
            }
        }
    }
}
</script>

<style scoped>
     button {
        opacity: 85%
    }
    button:hover {
        opacity: 100%
    }
</style>