<template>
  <div
    class="container"
    :class="clicked && 'clicked'"
    @click="handleClick"
  >
    <div class="logo" :data-content="content">{{ content }}</div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  position: fixed;
  right: 50%; top: 70%;
  z-index: 11;
  transform: translate(50%, -50%);
  transition:
    transform $t-long,
    inset $t-long;
  will-change: inset;

  &.clicked {
    right: 6%; top: 60px;
    transform: scale(1.5);
  }
}

.logo {
  cursor: pointer;
  position: relative;
  color: #f0f;
  mix-blend-mode: darken;
  max-width: max-content;
  font-size: MAX(16px, 4vw);
  --distance: -0.04em;
  transition: transform $t;

  &:hover {
    transform: scale(1.015);

    &::before { left: 0; top: 0; }
    &::after { right: 0; bottom: 0; }
  }

  @mixin logo {
    content: attr(data-content);
    position: absolute;
    mix-blend-mode: darken;
    transition: inset $t;
  }

  &::before {
    @include logo;
    left: var(--distance); top: var(--distance);
    color: #ff0;
  }

  &::after {
    @include logo;
    right: var(--distance); bottom: var(--distance);
    color: #0ff;
  }
}
</style>

<script>
export default {
  props: ['content', 'clicked', 'handleClick']
}
</script>
