<template>
  <section class="section circles">
    <circle-item
      v-for="item in items"
      :key="item.id"
      :item="item"
    />
  </section>
</template>

<script lang="ts">
import CircleItem from './CircleItem.vue'
export default {
  components: {
    CircleItem,
  },
  data() {
    return {
      items: [
        {
          id: 2,
          maxValue: 108,
          value: 108,
          targetValue: 80,
        },
        {
          id: 3,
          maxValue: 108,
          value: 107,
          targetValue: 80,
        },
        {
          id: 4,
          maxValue: 108,
          value: 90,
          targetValue: 80,
        },
        {
          id: 5,
          maxValue: 108,
          value: 79,
          targetValue: 80,
        },
        {
          id: 6,
          maxValue: 108,
          value: 1,
          targetValue: 80,
        },

      ]
    }
  },
}
</script>

<style lang="scss">
  .circles {
    display: flex;
    gap: 20px;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    max-width: 1200px;
    padding: 30px;
    margin-inline: auto;
    background-color: var(--cBg);
    min-height: 100vh;
  }
</style>