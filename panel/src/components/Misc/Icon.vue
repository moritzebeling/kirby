<template>
  <span
    :aria-label="alt"
    :role="alt ? 'img' : null"
    :aria-hidden="!alt"
    :data-back="back"
    :data-size="size"
    :class="'k-icon k-icon-' + type"
  >
    <span v-if="isEmoji" class="k-icon-emoji">{{ type }}</span>
    <svg v-else :style="{ color: color }" viewBox="0 0 16 16">
      <use :xlink:href="'#icon-' + type" />
    </svg>
  </span>
</template>

<script>
export default {
  props: {
    alt: String,
    color: String,
    back: String,
    size: String,
    type: String
  },
  computed: {
    isEmoji() {
      return this.$helper.string.hasEmoji(this.type);
    }
  }
};
</script>

<style lang="scss">
.k-icon {
  position: relative;
  line-height: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.k-icon svg {
  width: 1rem;
  height: 1rem;
  -moz-transform: scale(1);
}
.k-icon svg * {
  fill: currentColor;
}
.k-icon[data-back="black"] {
  background: $color-gray-900;
  color: $color-white;
}
.k-icon[data-back="white"] {
  background: $color-white;
  color: $color-gray-900;
}
.k-icon[data-back="pattern"] {
  background: lighten($color-gray-900, 10%) url($pattern);
  color: $color-white;
}
[data-disabled] .k-icon[data-back="black"] {
  background-color: $color-gray-600;
}
[data-disabled] .k-icon[data-back="pattern"] {
  background: lighten($color-gray-600, 5%) url($pattern);
  svg {
    opacity: 1;
  }
}
.k-icon[data-size="medium"] svg {
  width: 2rem;
  height: 2rem;
}
.k-icon[data-size="large"] svg {
  width: 3rem;
  height: 3rem;
}
.k-icon-emoji {
  display: block;
  line-height: 1;
  font-style: normal;
  font-size: 1rem;
}

/* fix emoji alignment on high-res screens */
@media only screen and (-webkit-min-device-pixel-ratio: 2), not all, not all, not all, only screen and (min-resolution: 192dpi), only screen and (min-resolution: 2dppx) {
  .k-icon-emoji {
    font-size: 1.25rem;
  }
}

</style>
