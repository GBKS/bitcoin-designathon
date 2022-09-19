<template>
  <a
    :class="classObject"
    :style="styleObject"
    :href="link"
    target="_blank"
  >{{ label }}</a>
</template>

<script>
export default {

  props: [
    'link',
    'label',
    'color',
    'size'
  ],

  computed: {
    classObject() {
      const c = ['super-button']

      if(this.size) {
        c.push('-size')
      } else {
        c.push('-medium')
      }

      return c.join(' ')
    },

    styleObject() {
      const s = {}

      if(this.color) {
        s.backgroundColor = this.color
      }

      return s
    }
  }

}
</script>

<style lang="scss" scoped>

@import "@/assets/css/animations.scss";
@import "@/assets/css/mixins.scss";

.super-button {
  display: inline-block;
  position: relative;
  border: 2px solid var(--front);
  text-decoration: none;
  border-radius: 1000px;
  @include r('font-size', 18, 27);
  font-weight: 900;
  padding: 5px 50px 6px 50px;
  color: var(--front);

  svg {
    width: 25px;
    height: 25px;
    margin-right: 10px;
    vertical-align: middle;
    transform: translateY(-2px);
  }

  &:nth-child(2) {
    padding-left: 15px;
    padding-right: 15px;
    text-align: center;

    svg {
      margin-right: 0;
    }
  }

  &:before {
    display: block;
    content: '';
    border: 2px solid rgba(var(--frontRGB), 0.2);
    position: absolute;
    left: -10px;
    top: -10px;
    width: calc(100% + 16px);
    height: calc(100% + 16px);
    pointer-events: none;
    border-radius: 1000px;
    transition: all 150ms ease-in-out;
  }

  &:hover {
    animation: buttonHover 500ms infinite $easeInOutSine alternate;

    &:before {
      left: -6px;
      top: -6px;
      width: calc(100% + 8px);
      height: calc(100% + 8px);
    }
  }
}

@keyframes buttonHover {
  0% {
    transform: scale(1, 1);
  }

  100% {
    transform: scale(1.05, 1.05);
  }
}

</style>