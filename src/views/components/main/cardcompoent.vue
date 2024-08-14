<template>
  <div style="margin: 5% 10%;">
    <div class="row row-cols-1 row-cols-md-3 g-4">
      <div
        class="col"
        v-for="job in curatedJobs"
        :key="job.jobId"
        style="border: 1px solid black; margin: 15px; box-shadow: 5px 5px 5px;"
      >
        <div class="card h-100">
          <img
            src="../../../../public/img/brand/mang.png"
            class="card-img-top"
            alt="Job Image"
          />
          <div class="card-body">
            <h5 class="card-title">{{ job.jobInfoTitle }}</h5>
            <p class="card-text">
              <strong>Company:</strong> {{ job.jobCompanyName }}<br />
              <strong>Location:</strong> {{ job.jobLocation }}<br />
              <strong>Wage Type:</strong> {{ job.jobWageType }}<br />
              <strong>Salary:</strong> {{ job.jobSalary }}<br />
              <!-- <strong>Web Info:</strong> <a :href="job.jobWebInfoUrl" target="_blank">{{ job.jobWebInfoUrl }}</a><br />
              <strong>Mobile Info:</strong> <a :href="job.jobMobileInfoUrl" target="_blank">{{ job.jobMobileInfoUrl }}</a> -->
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      jobs: [], // 전체 Job 데이터를 저장할 배열
      curatedJobs: [], // 큐레이션된 Job 데이터를 저장할 배열
    };
  },
  mounted() {
    this.fetchJobs(); // 컴포넌트가 마운트되면 데이터를 가져옵니다
  },
  methods: {
    async fetchJobs() {
      try {
        // 전체 데이터를 가져오는 API 호출
        const response = await axios.get('http://localhost:8083/api/jobs');
        this.jobs = response.data; // API로부터 받은 JobEntity 데이터를 저장합니다
        this.curateJobs(); // 큐레이션된 데이터 필터링
      } catch (error) {
        console.error('Error fetching job data:', error);
      }
    },
    curateJobs() {
      const curatedIds = [101, 102, 103, 104]; // 큐레이션된 ID 목록
      this.curatedJobs = this.jobs.filter(job => curatedIds.includes(job.jobId)); // 큐레이션된 데이터만 필터링
    },
  },
};
</script>
