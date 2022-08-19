<template>
<div class="app">
{{response}}
</div>
</template>

<script>
export default {
  name: "GlobalResult",

  props:{
    response:{
      type:Array,
      required:true
    }
  }
}
</script>

<style scoped>

</style>