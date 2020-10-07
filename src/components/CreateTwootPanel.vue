<template>
  <form class="create-twoot-panel" @submit.prevent="createNewTwoot" :class="{ '--exceeded': newTwootCharacterCount > 180 }">
    <label for="newTwoot"><strong>New Twoot</strong> ({{ newTwootCharacterCount }}/180)</label>
    <textarea id="newTwoot" rows="4" v-model="newTwootContent" />

    <div class="create-twoot-panel__type">
      <label for="newTwootType"><strong>Type</strong></label>
      <select id="newTwootType" v-model="selectedTwootType">
        <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
          {{ option.name }}
        </option>
      </select>
    </div>

    <button>Twoot</button>
  </form>
</template>

<script>
export default {
  name: 'CreateTwootPanel',
  data() {
    return {
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [
        { value: 'draft', name: 'Draft' },
        { value: 'instant', name: 'Instant Twoot' }
      ]
    }
  },
  computed: {
    newTwootCharacterCount() {
      return this.newTwootContent.length;
    }
  },
  methods: {
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== 'draft') {
        this.$emit('add-twoot', this.newTwootContent);
        this.newTwootContent = '';
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.create-twoot-panel {
  padding-top: 20px;
  display: flex;
  flex-direction: column;

  &.--exceeded {
    color: red;
    border-color: red;

    button {
      background: red;
      border: none;
      color: white;
    }
  }
}
</style>