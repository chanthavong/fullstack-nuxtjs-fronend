<template>
  <div>
    {{docs}}
  </div>
</template>

<script>
export default {
  data() {
    return {
      docs:[]
    }
  },
  mounted(){
    this.getDoc()
  },
  methods: {
    async getDoc() {
      let  rs = await this.$axios.get('doc')
      this.docs = rs.data.docs
    }
  },
}
</script>

<style>

</style>