<script>

import Base64 from '../assets/Base64.js'

const b = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/='
const hex = '䷁䷗䷆䷒䷎䷣䷭䷊䷏䷲䷧䷵䷽䷶䷟䷡䷇䷂䷜䷻䷦䷾䷯䷄䷬䷐䷮䷹䷞䷰䷛䷪䷖䷚䷃䷨䷳䷕䷑䷙䷢䷔䷿䷥䷷䷝䷱䷍䷓䷩䷺䷼䷴䷤䷸䷈䷋䷘䷅䷉䷠䷌䷫䷀☯'

export default {
  algo: {
    encode (text) {
      const uint8 = new TextEncoder('utf-8').encode(text)
      const b64r = Base64.encode(uint8)
      let result = ''
      for (const i of b64r) {
        result += hex[b.indexOf(i)]
      }
      return result
    },
    decode (text) {
      const uint8 = new TextDecoder('utf-8')
      let result = ''
      for (const i of text) {
        result += b[hex.indexOf(i)]
      }
      return uint8.decode(Base64.decode(result))
    }
  }
}
</script>
