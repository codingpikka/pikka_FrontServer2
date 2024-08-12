<template>
    <div v-if="job">
      <h1>{{ job.jobInfoTitle }}</h1>
      <p>Company: {{ job.jobCompanyName }}</p>
      <p>Location: {{ job.jobLocation }}</p>
      <p>Wage Type: {{ job.jobWageType }}</p>
      <p>Salary: {{ job.jobSalary }}</p>
      <p>Employment Type: {{ job.jobEmploymentType }}</p>
      <p>Web Info: <a :href="job.jobWebInfoUrl" target="_blank">{{ job.jobWebInfoUrl }}</a></p>
      <p>Mobile Info: <a :href="job.jobMobileInfoUrl" target="_blank">{{ job.jobMobileInfoUrl }}</a></p>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </template>
  

  <script>
import axios from 'axios';
import { ref, onMounted } from 'vue';

export default {
  name: 'JobDetailContent',
  props: {
    id: {
      type: String,
      required: true
    }
  },
  setup(props) {
    const job = ref(null); // job 변수를 ref로 반응형으로 선언

    onMounted(async () => {
      try {
        const response = await axios.get(`http://localhost:8083/api/jobs/${job.id}`);
        job.value = response.data; // API에서 데이터를 받아온 후 job 변수에 할당
      } catch (error) {
        console.error('Error fetching job data:', error);
      }
    });

    return { job }; // setup에서 job 변수를 반환하여 template에서 접근 가능하게 함
  }
};
</script>
<!-- 

  <script>
  import axios from 'axios';
  import { ref, onMounted } from 'vue';

  
  export default {
    setup() {
      const job = ref(null);
      const route = useRoute();
      const jobId = route.params.id; // URL에서 jobId를 가져옵니다
  
      onMounted(async () => {
        try {
          const response = await axios.get(`http://localhost:8083/api/jobs/${jobId}`);
          job.value = response.data;
        } catch (error) {
          console.error('Error fetching job data:', error);
        }
      });
  
      return { job };
    }
  };
  </script> -->
