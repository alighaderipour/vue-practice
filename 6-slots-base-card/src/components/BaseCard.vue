<script>
export default {
  name: 'BaseCard',

}
</script>

<template>
  <div class="card-container">

    <slot name="header" v-if="$slots.header"></slot>
    <slot>
      <p>This is the default card body.</p>
    </slot>
    <slot name="footer" v-if="$slots.footer"></slot>

  </div>
</template>