<script>

import { $CHERU as Cheru } from '~/assets/cheru'
// github.com/Ice-Cirno/HoshinoBot/blob/master/hoshino/modules/priconne/cherugo.py

function valuesDecode (encodedString) {
  if (encodedString.substr(0, 4) !== '切噜～♪') {
    throw new Error('Not a valid cherugo')
  }
  return encodedString.substr(4).replace(/切[切卟叮咧哔唎啪啰啵嘭噜噼巴拉蹦铃]+/g, (che) => {
    return Cheru.decode(che.substr(1))
  })
}

function valuesEncode (rawString) {
  const newString = rawString.replace(/[^，。？！、…：“”,\\.\\?!\s]+/g, (word) => {
    return '切' + Cheru.encode(word)
  })
  return '切噜～♪' + newString
}

export default {
  algo: {
    encode (text) {
      return valuesEncode(text)
    },
    decode (text) {
      return valuesDecode(text)
    }
  }
}
</script>
