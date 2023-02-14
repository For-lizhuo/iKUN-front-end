<template>
  <div>
    <svg-icon icon-class="github" @click="goto"/>
  </div>
</template>

<script>
export default {
  name: 'iKUNGit',
  data() {
    return {
      url: 'https://github.com/yhx1001/iKUN_Graduation_Project'
    }
  },
  methods: {
    goto() {
      window.open(this.url)
    }
  }
}
</script>
