<template>
    <div>
      <section class="section section-shaped my-0 overflow-hidden">
        <div class="container pt-lg pb-300">
          <div class="row text-center justify-content-center">
            <div class="col-lg-10">
              <badge pill type="primary" class="my-4">New Topic</badge>
  
              <h2 class="display-3 text-gray mb-4">자격증 게시판인데 여기다가 뭘쓰지?</h2>
              <p class="lead text-gray">
                새로 올라온 취업 정보를 보여줍니다. 부트스태랩에 있는 형태대로 쓰려고 했습니다만, 우와 폰트 짱귀여워
                <br />
                여기는 취업 관련 내용이 올라오는 곳이라고 소개글을 작성해야지. 그래서 뭔가 깔쌈하게 정리된 취업정보를 볼 수 있는 화면으로 만들어야지.
              </p>
            </div>
          </div>
  
          <div class="row row-grid mt-5">
            <div class="col-lg-4" v-for="job in jobs" :key="job.jobId">
              <div class="card shadow border-0 mb-4">
                <div class="card-body py-5" style="min-height: 620px;">
                  <div class="icon icon-shape icon-shape-primary rounded-circle mb-4">
                    <icon name="ni ni-settings" size="lg" gradient="white" shadow round color="primary"></icon>
                  </div>
                  <h5 class="text-gray mt-3">{{ job.jobInfoTitle }}</h5>
                  <ul class="list-unstyled mt-3 mb-0">
                    <li><strong>Company:</strong> {{ job.jobCompanyName }}</li>
                    <li><strong>Location:</strong> {{ job.jobLocation }}</li>
                    <li><strong>Wage Type:</strong> {{ job.jobWageType }}</li>
                    <li><strong>Salary:</strong> {{ job.jobSalary }}</li>
                    <li><strong>Web Info:</strong> <a :href="job.jobWebInfoUrl" target="_blank">{{ job.jobWebInfoUrl }}</a></li>
                    <li><strong>Mobile Info:</strong> <a :href="job.jobMobileInfoUrl" target="_blank">{{ job.jobMobileInfoUrl }}</a></li>
                  </ul>
                </div>
              </div>
            </div>
    

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
        jobs: [], // Job 데이터를 저장할 배열
      };
    },
    mounted() {
      this.fetchJobs(); // 컴포넌트가 마운트되면 데이터를 가져옵니다
    },
    methods: {
      async fetchJobs() {
        try {
          const response = await axios.get('http://localhost:8083/api/jobs');
          this.jobs = response.data; // API로부터 받은 JobEntity 데이터를 저장합니다
        } catch (error) {
          console.error('Error fetching job data:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .text-gray {
    color: #6c757d !important;
  }
  
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
  </style>
  