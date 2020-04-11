<script>
import Base64 from '../assets/Base64.js'

export default {
  algo: {
    encode (text) {
      return Base64.encode(new TextEncoder('utf-8').encode(text))
    },
    decode (text) {
      return new TextDecoder('utf-8').decode(Base64.decode(text))
    }
  }
}
</script>
