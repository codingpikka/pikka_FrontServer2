<template>
  <div>
    <section class="section section-shaped my-0 overflow-hidden">
      <div class="container pt-lg pb-300">
        <div class="row text-center justify-content-center">
          <div class="col-lg-10">
            <badge pill type="primary" class="my-4">New Topic</badge>
            <h2 class="display-3 text-gray mb-4">취업 게시판</h2>
            <p class="lead text-gray">
              서울시 일자리센터 채용 정보를 보여줍니다. 여기에서 다양한 회사의 채용 정보를 확인할 수 있습니다.
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
          <div class="col-lg-3 col-md-6 mb-4" v-for="job in paginatedJobs" :key="job.jobId">
            <div class="card shadow border-0 h-100">
              <div class="card-body d-flex flex-column">
                <div class="icon icon-shape icon-shape-primary rounded-circle mb-4">
                  <icon name="ni ni-briefcase-24" size="lg" gradient="white" shadow round color="primary"></icon>
                </div>
                <h5 class="text-primary font-weight-bold mb-3">{{ job.jobInfoTitle }}</h5>
                <div class="text-gray flex-grow-1">
                  <p class="mb-0"><strong>회사:</strong> {{ job.jobCompanyName }}</p>
                  <p class="mb-0"><strong>위치:</strong> {{ job.jobLocation }}</p>
                  <p class="mb-0"><strong>급여 유형:</strong> {{ job.jobWageType }}</p>
                  <p class="mb-0"><strong>급여:</strong> {{ formatSalary(job.jobSalary) }}</p>
                </div>
                <a :href="job.jobWebInfoUrl" target="_blank" class="btn btn-primary btn-sm mt-3">상세 정보</a>
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
      jobs: [],
      filteredJobs: [],
      currentPage: 1,
      itemsPerPage: 16,
      searchQuery: ''
    };
  },
  computed: {
    paginatedJobs() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.filteredJobs.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.filteredJobs.length / this.itemsPerPage);
    }
  },
  mounted() {
    this.fetchJobs();
  },
  methods: {
    async fetchJobs() {
      try {
        const response = await axios.get('http://localhost:8083/api/jobs');
        this.jobs = response.data;
        this.filteredJobs = [...this.jobs];
      } catch (error) {
        console.error('Error fetching job data:', error);
      }
    },
    changePage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
      }
    },
    formatSalary(salary) {
      if (!salary) return '미정';
      return salary.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",") + '원';
    },
    handleSearch() {
      if (this.searchQuery.trim() === '') {
        this.filteredJobs = [...this.jobs];
      } else {
        const query = this.searchQuery.toLowerCase();
        this.filteredJobs = this.jobs.filter(job => 
          job.jobInfoTitle.toLowerCase().includes(query) ||
          job.jobCompanyName.toLowerCase().includes(query) ||
          job.jobLocation.toLowerCase().includes(query) ||
          job.jobWageType.toLowerCase().includes(query)
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
</style>