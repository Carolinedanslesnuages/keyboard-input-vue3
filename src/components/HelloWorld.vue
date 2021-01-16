<template>
<div class="form-wrapper rounded">
  <div class="relative">
    <input
      v-model="inputValue"
      class="bg-gray-100 shadow rounded border-0 p-3 outline-none"
      label="Date de naissance"
      placeholder="jj/mm/aaaa"
      @click="showKeyBoard = !showKeyBoard"
    />
  </div>
    <div
      v-show="showKeyBoard"
      class="picker-wrap"
    >
    <button 
      v-for="btn in btns" 
      :value="btn.value" 
      :key="btn.id"
      class="button-numeric"
      @click="setValue(btn)"
    >
    {{btn.number}}
    </button>
    </div>
</div>
</template>

<script>
  import { ref, reactive } from 'vue'

  export default {
    setup() {
      const showKeyBoard = ref(Boolean)
      const inputValue = ref('')
      const btns = reactive([
        { number: '1', value: 1 },
        { number: '2', value: 2 },
        { number: '3', value: 3 },
        { number: '4', value: 4 },
        { number: '5', value: 5 },
        { number: '6', value: 6 },
        { number: '7', value: 7 },
        { number: '8', value: 8 },
        { number: '9', value: 9 },
        { number: '/', value: '/'},
        { number: '0', value: '0'},
        { number: 'C', value: '' },
      ])
    const setValue = (btn) => {
      if( btn.number === 'C') {
        return inputValue.value = ''
      }
      inputValue.value += btn.value
    }
      // expose to template
      return {
        btns,
        inputValue,
        showKeyBoard,
        setValue
      }
    }
  }
</script>
<style lang="postcss" scoped>
.form {
max-width: 32rem;
}
.form-wrapper {
  @apply shadow-md  py-2  mx-4  bg-blue-300 flex-grow;

position: fixed;
margin: 3em;
padding: 3em;
width: 46%;
display: flex;
justify-content: center;

  @media (max-width: 767px) {
    font-size: 0.75rem;
  }
}
.picker-wrap {
   @apply rounded  bg-blue-100;
  position: absolute;
  width: 200px;
  height: 255px;
  margin: 3.2em;
  box-shadow: 0 0 6px #ccc;
}

.button-numeric {
  @apply rounded  bg-blue-400  text-white  font-bold  py-2  m-2 ;

  height: 3em;
  width: 3em;

  &:hover {
    @apply bg-gray-500;
  }
}
</style>