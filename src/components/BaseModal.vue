<template>
  <div :style="modal">
    <div class="backdrop" @click="$emit('close')"></div>
    <div :style="modalContent" class="modalContent">
      <div :style="modalHeader">
          <h2>Cart</h2>
        <div class="closeButton"  @click="$emit('close')">
          <span class="material-icons">
            close
          </span>
        </div>
      </div>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    display: { default: "flex" },
    justifyContent: { default: "space-between" },
    padding: { default: "1rem"},
    zIndex: {default: "5"},
    
  },
  computed: {
    modal() {
      return {
        display: this.display,
        justifyContent: "flex-end",
        top: "0",
        width: "100%",
        position: "fixed"
      };
    },
    modalContent () {
        return {
            zIndex: this.zIndex,
            height: "100vh",
            background: "white",
            position: "fixed",
            display: "flex",
            flexDirection: "column",
            width: "20rem",
            borderRadius: "1rem"
        }
    },
    modalHeader() {
        return {
            display: this.display,
            justifyContent: this.justifyContent,
            padding: this.padding,
            alignItems: "center"
        }
    }
  },
};
</script>

<style scoped>
.backdrop {
  z-index: 4;
  top: 0;
  left: 0;
  background: grey;
  opacity: 0.1;
  width: 100vw;
  height: 100vh;
  position: fixed;
  cursor: pointer;
}
.closeButton {
  padding: 1rem;
  cursor: pointer;
}
</style>
