<template>
  <div style="margin: 5% 10%;">
    <div class="row row-cols-1 row-cols-md-3 g-4">
      <div
        class="col"
        v-for="job in jobs"
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
              <strong>Web Info:</strong> <a :href="job.jobWebInfoUrl" target="_blank">{{ job.jobWebInfoUrl }}</a><br />
              <strong>Mobile Info:</strong> <a :href="job.jobMobileInfoUrl" target="_blank">{{ job.jobMobileInfoUrl }}</a>
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
