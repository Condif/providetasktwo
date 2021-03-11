<template>
  <div :style="card">
    <div :style="cardContent">
        <slot></slot>
    </div>
  </div>
</template>

<script>

export default {
    props: {
        cardDisplay: {default: "grid"},
        gridTemplateColumns: {default: "repeat(auto-fit, minmax(150px, 1fr))"},
        display: {default: "flex"},
        flex: {default: "1 1 150px"},
        margin: {default: "5px"},
        flexDirection: {default: "column"},
        justifyContent: {default: "space-between"},
        padding: {default: "1rem"},
        borderRadius: {default: "1rem"},
        background: {default: "rgb(252, 252, 252)"},
        boxShadow: {default: "none"},
    },
    computed: {
        cardContent() {
            return {
                display: this.display,
                flex: this.flex,
                margin: this.margin,
                flexDirection: this.flexDirection,
                justifyContent: this.justifyContent,
                padding: this.padding,
                borderRadius: this.borderRadius,
                background: this.background,
            }
        },
        card() {
            return {
                display: this.cardDisplay,
                gridTemplateColumns: this.gridTemplateColumns,
                boxShadow: this.boxShadow
            }
        }
    }
}
</script>