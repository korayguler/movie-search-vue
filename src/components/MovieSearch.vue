<template>
  <input
    type="text"
    autofocus
    placeholder="Film adını yazın ve enter tuşuna basın..."
    class="search_text"
    v-model="searchValue"
    @keypress.enter="searchTrigger"
  />
</template>
<script>
export default {
  data() {
    return {
      searchValue: null,
    };
  },
  methods: {
    searchTrigger() {
      this.$emit('searchTrigger', this.searchValue);
    },
  },
};
</script>
