
<template>
    <div>

   
    <CertiContent></CertiContent>
    <router-view></router-view>


    </div>
 
</template>

<script>

import CertiContent from './components/certification/CertifiContent.vue';



export default {
  name: "jobPage",
  components: {
    
    CertiContent
  }
};

</script>
