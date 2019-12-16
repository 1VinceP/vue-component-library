<script>
import {
  Button, Input, Modal,
} from './components/common';

export default {
  name: 'app',
  data: () => ({
    searchValue: 'words here',
    validationValue: '',
    textareaValue: '',
    searching: false,

    modalOpen: false,
    successModalOpen: false,
    warningModalOpen: false,
    errorModalOpen: false,
  }),

  methods: {
    onSearch() {
      this.searching = true;
      setTimeout(() => {
        this.searching = false;
      }, 2000);
    },
  },

  components: {
    Button, Input, Modal,
  },
};
</script>

<template>
  <div id="app">
    <section class="buttons section">
      <Button primary>Primary</Button>
      <Button>Secondary</Button>
      <Button green>Success</Button>
      <Button orange>Warning</Button>
      <Button red>Error</Button>
      <Button link>Link</Button>
    </section>

    <section class="inputs section">
      <Input
        v-model="searchValue"
        buttonLabel="Search"
        :loading="searching"
        @button="onSearch"
      />
      <Input
        v-model="validationValue"
        label="Text box"
        required
        placeholder="Blur to show error"
        errorMessage="Text box cannot be empty"
        :validation="value => value !== ''"
      />
      <Input
        v-model="textareaValue"
        textarea
        liveValidation
        label="Text area"
        placeholder="These can have errors too. Type 'dog' to see"
        errorMessage="You cannot have a dog."
        :validation="value => !value.includes('dog')"
        :errorOnBlur="false"
      />
    </section>

    <section class="modals buttons section">
      <Button primary @click="modalOpen = true">Open Modal</Button>
      <Button green @click="successModalOpen = true">Open Modal</Button>
      <Button orange @click="warningModalOpen = true">Open Modal</Button>
      <Button red @click="errorModalOpen = true">Open Modal</Button>
    </section>

    <Modal
      :show="modalOpen"
      top
      title="Basic Modal"
      primaryLabel="Close"
      @primary="modalOpen = false"
    >
      This is a basic modal for displaying information.{{' '}}
      Check out the other examples to see what else you can do!
    </Modal>
    <Modal
      :show="successModalOpen"
      type="success"
      title="Success Modal"
      primaryLabel="Ok"
      @primary="successModalOpen = false"
    >
      This is a success modal, for sharing good news with your users.
    </Modal>
    <Modal
      :show="warningModalOpen"
      type="warning"
      title="Warning Modal"
      primaryLabel="Go Head"
      @primary="warningModalOpen = false"
      secondaryLabel="cancel"
      @secondary="warningModalOpen = false"
    >
      This is a warning modal, for alerting your users about something.
    </Modal>
    <Modal
      :show="errorModalOpen"
      type="error"
      title="Error Modal"
      primaryLabel="I know what I'm doing"
      @primary="errorModalOpen = false"
      secondaryLabel="Nevermind"
      @secondary="errorModalOpen = false"
      prompt
    >
      This is a error modal, for alerting users about something serious.<br />
      Type "dog" to confirm.
    </Modal>
  </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Nunito&display=swap');

* { font-family: 'Nunito', sans-serif; }

.buttons {
  width: 100%;
  display: flex;
  & button { margin-right: 20px; }
}

.section {
  margin-bottom: 60px;
}
</style>
