<template>
    <div>
      <section class="section section-shaped my-0 overflow-hidden">
        <div class="container pt-lg pb-300">
          <div class="row text-center justify-content-center">
            <div class="col-lg-10">
              <badge pill type="primary" class="my-4">New Topic</badge>
              <h2 class="display-3 text-gray mb-4">자격증 게시판</h2>
              <p class="lead text-gray">
                새로 올라온 취업 정보를 보여줍니다. 여기에서 다양한 회사의 채용 정보를 확인할 수 있습니다.
                최신 취업 트렌드와 기회를 놓치지 마세요!
              </p>
            </div>
          </div>
          
          <div class="row justify-content-center mt-4 mb-5">
            <div class="col-md-6">
              <div class="input-group">
                <input type="text" class="form-control" placeholder="검색어를 입력하세요" v-model="searchQuery" @input="handleSearch">
                <div class="input-group-append">
                  <button class="btn btn-primary" type="button" @click="handleSearch">검색</button>
                </div>
              </div>
            </div>
          </div>
          
          <div class="row row-grid mt-5">
            <div class="col-lg-3 col-md-6 mb-4" v-for="cafe in paginatedCafes" :key="cafe.jobId">
              <div class="card shadow border-0 h-100">
                <img :src="cafe.fileName" class="card-img-top" alt="Cafe Image">
                <div class="card-body d-flex flex-column">
                  <h5 class="text-primary font-weight-bold mb-3">{{ cafe.cafeName }}</h5>
                  <div class="text-gray flex-grow-1">
                    <p class="mb-0"><strong>소개:</strong> {{ cafe.simpleIntro }}</p>
                    <p class="mb-0"><strong>종류:</strong> {{ cafe.cafeType }}</p>
                    <p class="mb-0"><strong>운영시간:</strong> {{ cafe.useDate }}</p>
                    <p class="mb-0"><strong>주소:</strong> {{ cafe.baseAddress }}</p>
                    <p class="mb-0"><strong>도로명 주소:</strong> {{ cafe.roadAddress }}</p>
                  </div>
                  <a :href="cafe.fileName" target="_blank" class="btn btn-primary btn-sm mt-3">상세 정보</a>
                </div>
              </div>
            </div>
          </div>
          
          <div class="row justify-content-center mt-4">
            <nav aria-label="Page navigation">
              <ul class="pagination">
                <li class="page-item" :class="{ disabled: currentPage === 1 }">
                  <a class="page-link" href="#" @click.prevent="changePage(currentPage - 1)">이전</a>
                </li>
                <li class="page-item" v-for="page in totalPages" :key="page" :class="{ active: currentPage === page }">
                  <a class="page-link" href="#" @click.prevent="changePage(page)">{{ page }}</a>
                </li>
                <li class="page-item" :class="{ disabled: currentPage === totalPages }">
                  <a class="page-link" href="#" @click.prevent="changePage(currentPage + 1)">다음</a>
                </li>
              </ul>
            </nav>
          </div>
        </div>
      </section>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        cafes: [],
        filteredCafes: [],
        currentPage: 1,
        itemsPerPage: 16,
        searchQuery: ''
      };
    },
    computed: {
      paginatedCafes() {
        const start = (this.currentPage - 1) * this.itemsPerPage;
        const end = start + this.itemsPerPage;
        return this.filteredCafes.slice(start, end);
      },
      totalPages() {
        return Math.ceil(this.filteredCafes.length / this.itemsPerPage);
      }
    },
    mounted() {
      this.fetchCafes();
    },
    methods: {
      async fetchCafes() {
        try {
          const response = await axios.get('http://localhost:8083/api/jobcafes');
          this.cafes = response.data;
          this.filteredCafes = [...this.cafes];
        } catch (error) {
          console.error('Error fetching cafe data:', error);
        }
      },
      changePage(page) {
        if (page >= 1 && page <= this.totalPages) {
          this.currentPage = page;
        }
      },
      handleSearch() {
        if (this.searchQuery.trim() === '') {
          this.filteredCafes = [...this.cafes];
        } else {
          const query = this.searchQuery.toLowerCase();
          this.filteredCafes = this.cafes.filter(cafe =>
            cafe.cafeName.toLowerCase().includes(query) ||
            cafe.simpleIntro.toLowerCase().includes(query) ||
            cafe.cafeType.toLowerCase().includes(query) ||
            cafe.baseAddress.toLowerCase().includes(query)
          );
        }
        this.currentPage = 1;
      }
    }
  };
  </script>
  
  <style scoped>
  .card {
    border-radius: 0.75rem;
    transition: transform 0.3s ease-in-out;
  }
  
  .card:hover {
    transform: translateY(-10px);
  }
  
  .icon-shape-primary {
    background-color: #5e72e4;
    color: white;
  }
  
  .icon-shape {
    width: 3rem;
    height: 3rem;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .pagination {
    justify-content: center;
  }
  
  .text-primary {
    color: #5e72e4 !important;
  }
  
  .text-gray {
    color: #6c757d !important;
  }
  
  .card-body {
    padding: 1.5rem;
  }
  
  .btn-primary {
    background-color: #5e72e4;
    border-color: #5e72e4;
  }
  
  .btn-primary:hover {
    background-color: #4f5fbe;
    border-color: #4f5fbe;
  }
  
  .input-group {
    margin-bottom: 2rem;
  }
  
  .card-img-top {
    height: 200px;
    object-fit: cover;
  }
  </style>
  