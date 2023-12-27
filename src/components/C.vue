<template>
  <div>
    <slot :msg="msg"/>
  </div>
</template>

<script>
export default {
  name: 'C-component',
  data() {
    return {
      msg: 'Решение задачи №2'
    }
  }
};
</script>

<style scoped>

</style>
