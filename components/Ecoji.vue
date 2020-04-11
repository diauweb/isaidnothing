<template>
  <div>
    <p class="rounded-full bg-orange-300 inline-block p-2 px-4">
      <b>Known Issue:</b>  Currently can't process Unicode contents.
    </p>
    <p class="p-4 inline-block"></p>
  </div>
</template>

<script>

import * as Ecoji from '../node_modules/ecoji-js/dist/index.js'

export default {
  algo: {
    decode (text) {
      return Ecoji.decode(text)
    },
    encode (text) {
      return Ecoji.encode(text)
    }
  }
}

</script>
