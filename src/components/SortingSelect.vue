<template>
<label for="sorting">Sort by: &nbsp;</label>
  <select @change="$emit('sortingOption', $event.target.value)" name="sorting" id="sorting">
      <option >--</option>
      <option value="priceAsc">Price: Low to High</option>
      <option value="priceDesc">Price: High to Low</option>
      <option value="ratings">Best ratings</option>
  </select>
</template>

<script>
export default {
    name: 'SortingSelect',
    emits: ['sortingOption'],
}
</script>

<style scoped>

</style>