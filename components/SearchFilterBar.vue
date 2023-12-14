<script setup>

  let categoryList = categories.map(cat => {
    return {
      id: cat.id,
      // isEnabled: ref(true)
    }
  });
  
  // const toggleMethod = (categoryId) => {
  //   categoryList[categoryId - 1].disabled.value = true;

  //   console.log(categoryList);
  // }
  // const searchString = ref('');

  const emit = defineEmits(['tagToggle', 'searchInput']);

  const handleTagChange = (id, checked) => {
    emit('tagToggle', id, checked);

    // const currentCategory = categoryList.find(category => category.id === id);
    // currentCategory.isEnabled.value = !currentCategory.isEnabled.value;
  }

  const handleSearchInput = event => {
    // console.log(event.target.value)
    emit('searchInput', event.target.value);
  }

</script>

<template>
  <div class="bar">
    <input
      class="search"
      placeholder="Zoeken..."
      @keyup="handleSearchInput"
      />
      
    <!-- v-model="searchString" -->
    <!-- :isDisabled="category.isDisabled.value" -->
    <div>
      <CategoryTag
        v-for="category in categoryList"
        :categoryId="category.id"
        @toggle="handleTagChange"
      />
    </div>
  </div>
</template>

<style>
  .bar {
    display: flex;
    align-items: center;
    gap: 1rem;
    border-bottom: solid 1px var(--c-gray-100);
    padding: 1rem 0;
  }

  .search {
    font-size: 1rem;
    border-radius: 100rem;
    border: solid 1px var(--c-gray-100);
    padding: .5rem 1rem;
  }

  .search::placeholder {
    color: var(--c-gray-100);
  }
</style>