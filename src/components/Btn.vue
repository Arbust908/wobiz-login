<template>
  <button
    :type="type"
    :class="[btnType, btnSize, btnHover]"
    class="btn"
    @mouseenter="isHovered = true"
    @mouseleave="isHovered = false"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      default: "Button",
    },
    type: {
      type: String,
      default: "button",
    },
    color: {
      type: String,
      default: "primary",
    },
    isOutline: {
      type: Boolean,
      default: false,
    },
    size: {
      type: String,
      default: "normal",
      validator(value) {
        return ["lg", "sm", "normal"].indexOf(value) !== -1;
      },
    },
  },
  data() {
    return {
      isHovered: false,
    };
  },
  computed: {
    btnType() {
      return `btn-${this.isOutline ? "outline-" : ""}${this.color}`;
    },
    btnSize() {
      return this.size !== "normal" ? `btn-${this.size}` : null;
    },
    btnHover() {
      return this.isHovered ? "shadow" : null;
    },
  },
};
</script>
