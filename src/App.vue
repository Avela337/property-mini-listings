<template>
  <div id="app">
    
    <AppHeader :totalCount="filteredProperties.length" />

    <main class="main-container">
      
      <section class="controls-panel">
        <div class="search-wrapper">
          <input 
            v-model="searchQuery" 
            type="text" 
            placeholder="Search by title or location (e.g., Sea Point)..." 
            class="search-input"
          />
        </div>
        
        <div class="sort-wrapper">
          <label for="sortOrder" class="sort-label">Sort by Price:</label>
          <select id="sortOrder" v-model="sortOrder" class="sort-select">
            <option value="default">Featured</option>
            <option value="low-to-high">Price: Low to High</option>
            <option value="high-to-low">Price: High to Low</option>
          </select>
        </div>
      </section>

      
      <div v-if="filteredProperties.length === 0" class="empty-state">
        <p>No listings matched your criteria. Try adjusting your query search.</p>
      </div>

      
      <section v-else class="property-grid">
        <PropertyCard 
          v-for="item in filteredProperties" 
          :key="item.id" 
          :property="item"
          :isBookmarked="bookmarks.includes(item.id)"
          @toggle-bookmark="handleBookmarkToggle"
        />
      </section>
    </main>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import PropertyCard from './components/PropertyCard.vue';
import { initialProperties } from './mockData';

export default {
  name: 'App',
  components: {
    AppHeader,
    PropertyCard
  },
  data() {
    return {
      properties: initialProperties,
      searchQuery: '',
      sortOrder: 'default',
      
      bookmarks: JSON.parse(localStorage.getItem('property_bookmarks')) || []
    }
  },
  computed: {
    
    filteredProperties() {
      let result = [...this.properties];

      
      if (this.searchQuery.trim() !== '') {
        const query = this.searchQuery.toLowerCase().trim();
        result = result.filter(item => 
          item.title.toLowerCase().includes(query) || 
          item.location.toLowerCase().includes(query)
        );
      }

      
      if (this.sortOrder === 'low-to-high') {
        result.sort((a, b) => a.price - b.price);
      } else if (this.sortOrder === 'high-to-low') {
        result.sort((a, b) => b.price - a.price);
      }

      return result;
    }
  },
  methods: {
    handleBookmarkToggle(propertyId) {
      const index = this.bookmarks.indexOf(propertyId);
      if (index > -1) {
        this.bookmarks.splice(index, 1); // Remove
      } else {
        this.bookmarks.push(propertyId); // Add
      }
      
      localStorage.setItem('property_bookmarks', JSON.stringify(this.bookmarks));
    }
  }
}
</script>

<style>

* {
  box-sizing: border-box;
}
body {
  margin: 0;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  background-color: #f7fafc;
  color: #2d3748;
  -webkit-font-smoothing: antialiased;
}
.main-container {
  max-width: 1200px;
  margin: 2rem auto;
  padding: 0 1.5rem;
}


.controls-panel {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin-bottom: 2rem;
  background: white;
  padding: 1.25rem;
  border-radius: 10px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.05);
  align-items: center;
}
.search-wrapper {
  flex-grow: 1;
}
.search-input {
  width: 100%;
  padding: 0.75rem 1rem;
  font-size: 0.95rem;
  border: 1px solid #cbd5e0;
  border-radius: 6px;
  outline: none;
  transition: border-color 0.2s;
}
.search-input:focus {
  border-color: #3182ce;
  box-shadow: 0 0 0 3px rgba(66, 153, 225, 0.15);
}
.sort-wrapper {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.sort-label {
  font-size: 0.9rem;
  color: #4a5568;
  font-weight: 500;
  white-space: nowrap;
}
.sort-select {
  padding: 0.75rem 2rem 0.75rem 1rem;
  font-size: 0.95rem;
  border: 1px solid #cbd5e0;
  border-radius: 6px;
  background-color: white;
  cursor: pointer;
}


.property-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

.empty-state {
  text-align: center;
  padding: 3rem;
  background: white;
  border-radius: 10px;
  color: #718096;
  border: 2px dashed #e2e8f0;
}
</style>
