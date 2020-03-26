<script>

import * as Base65536 from '~/node_modules/base65536/dist/es6/base65536.js'

export default {
  algo: {
    encode (text) {
      const uint8 = new TextEncoder('utf-8').encode(text)
      return Base65536.encode(uint8)
    },
    decode (text) {
      const uint8 = new TextDecoder('utf-8')
      return uint8.decode(Base65536.decode(text))
    }
  }
}
</script>
