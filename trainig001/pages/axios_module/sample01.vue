<template>
  <div>
    <h1>/axios_module/sample01</h1>
    <p>console.log() で、qiita API のアクセス結果を表示する</p>
  </div>
</template>

<script>
export default {
  async mounted(){
    /* 外部API(qiita api) をコールして内容を表示 */
    console.log(
      JSON.stringify(
        await this.$axios.$get('https://qiita.com/api/v2/items?query=tag:nuxt.js'),
        true,
        ' '
      )
    )
  }
}
</script>
