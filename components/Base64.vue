<script>
export default {
  algo: {
    encode (text) {
      return btoa(text)
    },
    decode (text) {
      return atob(text)
    }
  }
}
</script>
