<script setup>

  const members = [
    {
      id: 1,
      image: "vincent",
      name: "Vincent Schoutsen",
      description: "Kunstenaar, muzikant, event organisor",
      categories: [1, 2, 3],
      visible: ref(true)
    },
    {
      id: 2,
      image: "anke",
      name: "Anke Muijsers",
      description: "Grafisch ontwerp, visual researcher",
      categories: [3, 6],
      visible: ref(true)
    },
    {
      id: 3,
      image: "jet",
      name: "Jet Gerding",
      description: "Buurman, festivalbouwer, crewcatering",
      categories: [1, 4, 5],
      visible: ref(true)
    },
    {
      id: 4,
      image: "marnix",
      name: "Marnix Damsteeg",
      description: "Studio Antenne",
      categories: [2, 5],
      visible: ref(true)
    },
  ];

  const handleTagToggle = (categoryId, checked) => {
    members.forEach(member => {
      if(checked === false && member.categories.indexOf(categoryId) > -1) {
        member.visible.value = false;
      } else {
        member.visible.value = true;
      }
    })
  }

  const handleSearchInput = (searchText) => {
    members.forEach(member => {
      member.visible.value = false;

      const {name, description} = member;
      
      const lc = (text) => text.toLowerCase();

      if(
        lc(name).indexOf(lc(searchText)) > -1 ||
        lc(description).indexOf(lc(searchText)) > -1
      ) {
        member.visible.value = true;
      }
    })
  }
</script>

<template>
  <div class="main">
    <NuxtWelcome />
    
    <header class="header">  
      <NuxtImg class="logo animate-wiggle" src="logo.svg" />
      <div>
        <h1 class="title">HOFLEDEN</h1>
        <p>
          Het Hof van Cartesius is een coöperatie. Dat betekent dat de leden niet alleen huurders zijn, maar actief meedenken en werken aan de inrichting, beheer en de programmering van Het Hof.
        </p>
      </div>
    </header>

      <SearchFilterBar
        @tagToggle="handleTagToggle"
        @searchInput="handleSearchInput"
      />

    <ul class="member-list">
      <MemberItem
        v-for="member in members"
        :member="member"
      />
    </ul>

  </div>
</template>

<!-- Global styling -->
<style>

:root {
  --c-green-200: #449942;
  --c-gray-50: #f6f6f6;
  --c-gray-100: #ccc;
  --c-gray-200: #6B7280;
  --c-pink-100: #F4DADA;
  --c-yellow-100: #F2F486;
  --c-blue-100: #BFE9FC;
  --c-purple-100: #E2DAF4;
  --c-orange-100: #F4A786;
  --c-green-100: #E1FCBF;
  --c-cyan-100: #8EFFF8;
}

body {
  margin: 0;
  background: white;
  color: var(--c-gray-200);
  font-family: sans-serif;
}

h1,h2,h3 {
  color: var(--c-green-200);
}

@keyframes spin {
  to {
    rotate: 1turn;
  }
}

@keyframes wiggle {
  from {
    rotate: -10deg;
  }
  to {
    rotate: 10deg;
  }
}

</style>

<!-- App styling -->
<style scoped>
.main {
  padding: 2rem;
  max-width: 80rem;
  margin: 0 auto;
}

.header {
  margin: 0 auto;
  width: 48rem;
  display: flex;
  align-items: flex-start;
  gap: 2rem;
  padding: 3rem 0;
}

.logo {
  width: 8rem;
  /* position: absolute;
  top: 4rem;
  left: 4rem; */
}

.title {
  margin: 0;
  line-height: 1;
}

p {
  line-height: 1.5;
  max-width: 32rem;
}

.animate-spin {
  animation: spin 30s linear infinite;
}
.animate-wiggle {
  animation: wiggle 3s ease-in-out alternate infinite;
}

.member-list {
  display: flex;
  flex-direction: column;
  /* gap: 1.5rem; */
  padding: 1rem 0;
}

</style>
