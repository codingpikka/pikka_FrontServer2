
<template>
    <div>

    
    <PostContent></PostContent>
    <router-view></router-view>


    </div>
 
</template>

<script>
import PostContent from './components/post/PostContent.vue';



export default {
  name: "jobPage",
  components: {
    PostContent
  }
};

</script>