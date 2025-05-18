<template>
  <div class="news responsive-container">
    <h1>Latest News</h1>
    
    <!-- Search and filters -->
    <div class="row mb-4">
      <div class="col-md-6 mb-3">
        <div class="input-group">
          <input 
            type="text" 
            class="form-control" 
            placeholder="Search news..." 
            v-model="searchQuery"
            aria-label="Search news"
          >
        </div>
      </div>
      
      <div class="col-md-3 mb-3">
        <select class="form-select" v-model="categoryFilter">
          <option value="">All Categories</option>
          <option v-for="category in uniqueCategories" :key="category" :value="category">
            {{ category }}
          </option>
        </select>
      </div>
      
      <div class="col-md-3 mb-3">
        <input 
          type="date" 
          class="form-control" 
          v-model="dateFilter"
          aria-label="Filter by date"
        >
      </div>
    </div>
    
    <!-- News Items -->
    <div class="row">
      <div v-if="filteredNews.length === 0" class="col-12 text-center">
        <p>No news items found matching your search criteria.</p>
      </div>
      
      <div v-for="item in paginatedNews" :key="item.id" class="col-md-6 col-lg-4 mb-4">
        <NewsItem :news="item" />
      </div>
    </div>
    
    <!-- Pagination -->
    <div class="row">
      <div class="col-12">
        <nav aria-label="News pagination">
          <ul class="pagination justify-content-center">
            <li class="page-item" :class="{ disabled: currentPage === 1 }">
              <button class="page-link" @click="currentPage--" :disabled="currentPage === 1">
                Previous
              </button>
            </li>
            
            <li 
              v-for="page in totalPages" 
              :key="page" 
              class="page-item"
              :class="{ active: page === currentPage }"
            >
              <button class="page-link" @click="currentPage = page">{{ page }}</button>
            </li>
            
            <li class="page-item" :class="{ disabled: currentPage === totalPages }">
              <button 
                class="page-link" 
                @click="currentPage++" 
                :disabled="currentPage === totalPages"
              >
                Next
              </button>
            </li>
          </ul>
        </nav>
      </div>
    </div>
  </div>
</template>

<script>
import NewsItem from '../components/NewsItem.vue'
import newsData from '../data/news.json'

export default {
  name: 'NewsView',
  components: {
    NewsItem
  },
  data() {
    return {
      newsItems: [],
      searchQuery: '',
      categoryFilter: '',
      dateFilter: '',
      currentPage: 1,
      itemsPerPage: 6
    }
  },
  created() {
    this.newsItems = newsData
  },
  computed: {
    filteredNews() {
      let filtered = this.newsItems

      // Filter by search query
      if (this.searchQuery) {
        const query = this.searchQuery.toLowerCase()
        filtered = filtered.filter(item => 
          item.title.toLowerCase().includes(query) || 
          item.content.toLowerCase().includes(query)
        )
      }

      // Filter by category
      if (this.categoryFilter) {
        filtered = filtered.filter(item => item.category === this.categoryFilter)
      }

      // Filter by date
      if (this.dateFilter) {
        const filterDate = new Date(this.dateFilter)
        filtered = filtered.filter(item => {
          const itemDate = new Date(item.date)
          return itemDate.toDateString() === filterDate.toDateString()
        })
      }

      return filtered
    },
    totalPages() {
      return Math.ceil(this.filteredNews.length / this.itemsPerPage)
    },
    paginatedNews() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage
      const endIndex = startIndex + this.itemsPerPage
      return this.filteredNews.slice(startIndex, endIndex)
    },
    uniqueCategories() {
      const categories = this.newsItems.map(item => item.category)
      return [...new Set(categories)]
    }
  },
  watch: {
    filteredNews() {
      // Reset to page 1 when filters change
      this.currentPage = 1
    }
  }
}
</script>

<style scoped>
.pagination {
  margin-top: 2rem;
}
</style>