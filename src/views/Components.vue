<template>
  <div>
    <Sildcompoent></Sildcompoent>
    <announcementcompoent></announcementcompoent>
    <cardcompoent></cardcompoent>
  </div>
</template>
<script>
import Sildcompoent from "./components/main/Sildcompoent.vue";
import announcementcompoent from "./components/main/announcementcompoent.vue";
import cardcompoent from "./components/main/cardcompoent.vue";

export default {
  name: "components",
  components: {
    Sildcompoent,
    announcementcompoent,
    cardcompoent,
  },
};
</script>
