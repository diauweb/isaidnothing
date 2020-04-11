<script>

import * as Braille from '~/node_modules/braille-encode/index.js'

export default {
  algo: {
    encode (text) {
      const uint8 = new TextEncoder('utf-8').encode(text)
      return Braille.encode(uint8)
    },
    decode (text) {
      const uint8 = new TextDecoder('utf-8')
      return uint8.decode(Braille.decode(text))
    } 
  }
}
</script>
