<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <global-form></global-form>

  </div>
</template>

<script>
// @ is an alias to /src
import GlobalForm from "@/components/GlobalForm";


export default {
  name: 'HomeView',
  components: {
    GlobalForm,


  }
}
</script>
