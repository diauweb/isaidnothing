<template>
  <div class="flex-1 md:m-10 shadow-xl p-5 bg-white rounded-lg">
    <h1>I said nothing</h1>
    <h2>A tool for converting text to different representations.</h2>

    <div class="content-box">
      <p class="mb-2 mx-2 text-sm text-gray-500">SELECT METHOD</p>
      <Selector 
        v-for="tool in tools" 
        :key="tool.name"
        :class="[{ active: currentTool && currentTool.name === tool.name }]"
        @switch="switchTool(tool)">
        {{tool.displayName}}
      </Selector>
      <Selector class="selector-more">Adding more soon...</Selector>
    </div>
    <div class="content-box">
      <textarea class="text" v-model="input" placeholder="Input Text Here..."></textarea>
      <textarea 
        class="text"
        :style="{ color: resultFailed? 'red' : 'black' }"
        :value="result"
        :readonly="resultFailed"
        placeholder="Output" >
        </textarea>
      <div v-if="currentTool">
        <div class="option" v-if="currentTool.extended">
          <keep-alive>
            <component :is="currentTool.comp"></component>
          </keep-alive>
        </div>
        <div class="flex mt-5 mb-2">
          <button class="button rounded-l-full" @click="encode">Encode</button>
          <button class="button rounded-r-full" @click="decode">Decode</button>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import Selector from '~/components/Selector.vue'
import tools from '~/assets/tools.json'

export default {
  components: {
    Selector
  },
  data () {
    return {
      tools, 
      comps: {},
      input: "",
      result: "",
      resultFailed: false,
      currentTool: null
    }
  },
  created () {
    for (const i in tools) {
      const comp = import(`~/components/${this.tools[i].useComponent}`)
      comp.then(o => this.tools[i].comp = o.default)
    }
  },
  methods: {
    switchTool (me) {
      this.currentTool = me
    },
    encode () {
      this.result = this.currentTool.comp.algo.encode(this.input);
      this.resultFailed = false
    },
    decode () {
      try {
        this.result = this.currentTool.comp.algo.decode(this.input);
        this.resultFailed = false
      } catch {
        this.result = "Decode Failed"
        this.resultFailed = true
      }
    }
  }
}

</script>

<style lang="postcss"> 
  h1 {
    @apply text-4xl;
  }

  h2 {
    @apply text-xl text-gray-500;
  }

  .content-box {
    @apply mt-5 p-5 bg-gray-100 rounded-lg;
  }

  .text {
    @apply w-full bg-gray-200 rounded px-5 py-3 h-48;
  }
  
  .option {
    @apply w-full bg-gray-200 rounded px-5 py-3 pb-4 text-gray-800;
  }

  .button {
    @apply bg-blue-500 px-5 py-2 text-white inline-block;
    @apply cursor-pointer;
  }

  .button.active {
    @apply bg-blue-600 shadow;
    @apply border-2 box-border;
  }

  .button:hover {
    @apply bg-blue-600 shadow-md;
    @apply transition-shadow transition-colors duration-100;
  }

  .selector-more {
    @apply bg-gray-500 !important;
    @apply cursor-default;
  }

  .selector-more:hover {
    @apply shadow-none;
  }
</style>
