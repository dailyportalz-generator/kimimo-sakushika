<template>
  <form @submit.prevent="handleSubmit" class="select-question">
    <dl>
      <dt>まず、曲のタイトルを決めよう</dt>
      <dd>
        <select v-model="selectedValue[0]">
            <template v-for="(title, i) in titleListFirst">
                <option :key="title" :value="i+1">
                    {{title}}
                </option>
            </template>
        </select>
        <select v-model="selectedValue[1]">
            <template v-for="(title, i) in titleListSecond">
                <option :key="title" :value="i+1">
                    {{title}}
                </option>
            </template>
        </select>
      </dd>
    </dl>
    <button>次へ</button>
  </form>
</template>

<script>
export default {
  props: {
    titleListFirst: Array,
    titleListSecond: Array,
    value: Array
  },
  data() {
      return {
          selectedValue: this.value
      }
  },
  methods: {
      handleSubmit() {
          this.$emit('start', {
              index1: this.selectedValue[0],
              index2: this.selectedValue[1]
          })
      }
    }
}
</script>

<style scoped>
.select-question {
  margin-bottom: 24px;
  padding-bottom: 24px;
  border-bottom: dotted 1px #c6c6c6;
}

h3 {
  font-size: 1em;
}

dd {
  margin: 16px 0 0;
  padding: 0 0 8px 0;
}

button {
  width: 60px;
}

input[type='text'] {
  margin-right: 20px;
}
</style>