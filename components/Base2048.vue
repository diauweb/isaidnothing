<script>

import * as Base2048 from '~/node_modules/base2048/dist/es6/base2048.js'

export default {
  algo: {
    encode (text) {
      const uint8 = new TextEncoder('utf-8').encode(text)
      return Base2048.encode(uint8)
    },
    decode (text) {
      const uint8 = new TextDecoder('utf-8')
      return uint8.decode(Base2048.decode(text))
    }
  }
}
</script>
