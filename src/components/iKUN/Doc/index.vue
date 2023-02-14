<template>
  <div>
    <svg-icon icon-class="question" @click="goto"/>
  </div>
</template>

<script>
export default {
  name: 'iKUNDoc',
  data() {
    return {
      url: 'https://yhx1001.github.io/iKUN_docsify/#/'
    }
  },
  methods: {
    goto() {
      window.open(this.url)
    }
  }
}
</script>
