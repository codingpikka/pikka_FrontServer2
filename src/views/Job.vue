
<template>
    <div>

    
    <JobContent></JobContent>
    <router-view></router-view>


    </div>
 
</template>

<script>

import JobContent from './components/job/JobContent.vue';



export default {
  name: "jobPage",
  components: {
    JobContent
  }
};

</script>
