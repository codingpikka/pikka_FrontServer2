<template>
  <div>
    <section class="section section-shaped my-0 overflow-hidden">
      <div class="container pt-lg pb-300">
        <div class="row text-center justify-content-center">
          <div class="col-lg-10">
            <badge pill type="primary" class="my-4">New Topic</badge>
            <h2 class="display-3 text-gray mb-4">자격증 게시판</h2>
            <p class="lead text-gray">
              최신 자격증 정보를 한눈에 확인하세요. 다양한 분야의 자격증 정보를 제공하여
              여러분의 커리어 발전을 돕습니다. 관심 있는 자격증을 찾아 전문성을 키워보세요!
            </p>
          </div>
        </div>
        
        <div class="row row-grid mt-5">
          <div class="col-lg-3 col-md-6 mb-4" v-for="cert in paginatedCertifications" :key="cert.certId">
            <div class="card shadow border-0 h-100">
              <div class="card-body d-flex flex-column">
                <div class="icon icon-shape icon-shape-primary rounded-circle mb-4">
                  <icon name="ni ni-paper-diploma" size="lg" gradient="white" shadow round color="primary"></icon>
                </div>
                <h5 class="text-primary font-weight-bold mb-3">{{ cert.certName }}</h5>
                <div class="text-gray flex-grow-1">
                  <p class="mb-0"><strong>분야:</strong> {{ cert.certField }}</p>
                  <p class="mb-0"><strong>주관:</strong> {{ cert.certOrganization }}</p>
                  <p class="mb-0"><strong>등급:</strong> {{ cert.certLevel || '해당 없음' }}</p>
                  <p class="mb-0"><strong>접수기간:</strong> {{ formatDate(cert.certApplyStart) }} - {{ formatDate(cert.certApplyEnd) }}</p>
                </div>
                <a :href="cert.certInfoUrl" target="_blank" class="btn btn-primary btn-sm mt-3">상세 정보</a>
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
      certifications: [],
      currentPage: 1,
      itemsPerPage: 16
    };
  },
  computed: {
    paginatedCertifications() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.certifications.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.certifications.length / this.itemsPerPage);
    }
  },  
  mounted() {
    this.fetchCertifications();
  },
  methods: {
    async fetchCertifications() {
      try {
        const response = await axios.get('http://localhost:8083/api/jobs');
        // api 들어오는곳 수정 certification 데이터 값 확인을 위해 jobs로 연결해둠
        this.certifications = response.data;
      } catch (error) {
        console.error('Error fetching certification data:', error);
      }
    },
    changePage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
      }
    },
    formatDate(dateString) {
      if (!dateString) return '미정';
      const date = new Date(dateString);
      return `${date.getFullYear()}-${String(date.getMonth() + 1).padStart(2, '0')}-${String(date.getDate()).padStart(2, '0')}`;
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
</style>