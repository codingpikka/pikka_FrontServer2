<template>
    <div>
      <h1>Job List</h1>
      <ul>
        <li v-for="job in jobs" :key="job.jobId">
          <h2>{{ job.jobInfoTitle }}</h2>
          <p>Company: {{ job.jobCompanyName }}</p>
          <p>Location: {{ job.jobLocation }}</p>
          <p>Wage Type: {{ job.jobWageType }}</p>
          <p>Salary: {{ job.jobSalary }}</p>
          <p>Employment Type: {{ job.jobEmploymentType }}</p>
          <p>Web Info: <a :href="job.jobWebInfoUrl" target="_blank">{{ job.jobWebInfoUrl }}</a></p>
          <p>Mobile Info: <a :href="job.jobMobileInfoUrl" target="_blank">{{ job.jobMobileInfoUrl }}</a></p>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        jobs: [] // Job 데이터를 저장할 배열
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
      }
    }
  };
  </script>
  
  <style scoped>
  /* Add your styles here */
  </style>
  