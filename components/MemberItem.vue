<script setup>
  const props = defineProps({
    member: Object
  })

</script>

<template>
  <li :class="`row ${member.visible.value ? '' : 'hidden'}`">
    <header class="header">
      <NuxtImg class="avatar" :src="`images/${ member.image }.png`" />

      <div>
        <h2 class="heading">{{ member.name }}</h2>
        <p>{{ member.description }}</p>
        <div>
        <CategoryTag
          v-for="catId in member.categories"
          :categoryId="catId"
          :noText=false
        />
      </div>
      </div>
      
    </header>

    
    
  </li>
</template>

<style scoped>
  .row {
    display: flex;
    flex-direction: column;
    /* gap: 1rem; */
    /* padding-bottom: 2rem; */
    /* border-bottom: solid #eee 1px; */
    overflow: hidden;
    height: 8.5rem;
    transition:
      height .3s ease-in-out,
      margin-bottom .3s ease-in-out,
      opacity .4s ease-out;
    background: var(--c-gray-50);
    border-radius: 10px;
    margin-bottom: 1rem;
  }
  
  .row.hidden {
    height: 0;
    margin-bottom: 0;
    opacity: 0;
    pointer-events: none;
  }

  .row:last-child {
    /* border-bottom: none; */
  }
  
  .header {
    display: flex;
    align-items: flex-start;
    flex-direction: row;
    gap: 1rem;
    padding: 1rem;
  }

  .heading {
    margin: 0;
    line-height: 1;
    background: var(--c-green-200);
    color: white;
    padding: .3rem;
    display: inline;
    font-size: 1rem;
  }

  .avatar {
    overflow: hidden;
    border-radius: 100em;
    width: 6rem;
    aspect-ratio: 1;
  }
</style>