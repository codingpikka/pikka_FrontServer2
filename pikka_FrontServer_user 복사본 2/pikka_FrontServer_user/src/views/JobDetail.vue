// children 으로 어케 만들지?

<template>
    <div>
      <JobDetailContent :id="id"></JobDetailContent>


    </div>
 
 
</template>

<script>
import JobDetailContent from './components/job/JobDetailContent.vue';
import { ref } from 'vue';
import { useRoute } from 'vue-router';

export default {
  name: 'jobDetail',
  components: {
    JobDetailContent
  },
  setup() {
    const route = useRoute();
    const id = ref(route.params.id); // route.params에서 id를 가져옴

    return {
      id
    };
  }
};
</script>
<!-- <script>
import JobDetailContent from './components/job/JobDetailContent.vue';

export default {
  name: "jobDetail",
  components: {
    JobDetailContent
  }
};

</script> -->
