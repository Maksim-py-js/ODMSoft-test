<template>
  <ul class="to-do-list">
    <li
      :class="`to-do-list__item ${
        item.checked ? 'to-do-list__item_active' : ''
      }`"
      v-for="(item, index) in dataList"
      :key="index"
      @click="$emit('toggleItem', item.id)"
    >
      {{ item.name }}
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    dataList: {
      dafault: [],
    },
  },
};
</script>

<style lang="css">
.to-do-list__item_active {
  color: red;
}
</style>
