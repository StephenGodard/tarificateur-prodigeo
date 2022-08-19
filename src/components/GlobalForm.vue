<template>
<div>
  <b-container>
<get-current-coverage class="getCurrentCoverage"></get-current-coverage>

  </b-container>
</div>
</template>

<script>

import getCurrentCoverage from "@/components/Form/GetCurrentCoverage";
export default {
  name: "GlobalForm",
components:{getCurrentCoverage}
}
</script>

<style scoped>
.getCurrentCoverage{
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25);
  border-radius: 5px;
  padding:5%;
  min-width: 120px;

}

</style>