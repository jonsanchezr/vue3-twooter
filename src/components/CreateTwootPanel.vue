<template>
    <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot" :class="{'--exceeded': newTwootCharacterCount > 180 }">
        <label for="newTwoot"><strong>New Twoot</strong>({{newTwootCharacterCount}}/180)</label>
        <textarea id="newTwoot" rows="4" v-model="state.newTwootContent"></textarea>
        <div class="user-profile__create-twoot-type">
            <label for="newTwooType"><strong>Type: </strong></label>
            <select id="newTwootType" v-model="state.newSelectedType">
                <option :value="option.value" v-for="(option, index) in state.twootTypes" :key="index">
                {{ option.name }}
                </option>
            </select>
        </div>
        <button>
        Twoot!
        </button>
    </form>
</template>

<script>
import { reactive, computed } from 'vue';
export default {
  name: 'CreateTwootPanel',
  setup(props, ctx) {
      const state = reactive({
        newTwootContent: '',
        newSelectedType: 'instant',
        twootTypes: [
            {value: 'draft', name: 'Draft'},
            {value: 'instant', name: 'Instant'},
        ]
      });

      const newTwootCharacterCount = computed(() => state.newTwootContent.length);
      
      function createNewTwoot() {
        if (state.newTwootContent && state.newSelectedType !== 'draft') {
            ctx.emit('addtwoot', state.newTwootContent);
            state.newTwootContent = '';
        }
      }
      return {
          state,
          newTwootCharacterCount,
          createNewTwoot
      }
  }
}
</script>


<style scoped>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    grid-gap: 50px;
    padding: 50px 5%;
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile__admin-badge {
    background: rebeccapurple;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
    margin-bottom: 20px;
}

h1 {
    margin: 0;
}

.user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
}

.user-profile__create-twoot {
    border-top: 1px solid #DFE3E8;
    padding-top: 20px;
    display: flex;
    flex-direction: column;
}

.--exceeded {
  color:red;
  border-color: red;
}

.--exceeded button {
  background-color: red;
  border: none;
  color: white;
}
</style>
