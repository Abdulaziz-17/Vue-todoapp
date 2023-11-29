<template>
  <div class="modal" @click="close">
    <div class="modal__window" @click.stop>
      <h3 class="modal__title">
        {{ edit ? $t("titlewindowedit"): $t("titlewindow") }}
      </h3>
      <div class="modal__form">
        <label>
          <span>title</span>
          <input
            v-model="title"
            type="text"
            placeholder="title"
            class="modal__input"
          />
        </label>
        <label>
          <span>text</span>
          <input
            v-model="text"
            type="text"
            placeholder="text"
            class="modal__input"
          />
        </label>
      </div>
      <div class="modal__buttons">
        <button class="modal__btn del" @click="close">{{ $t("closebtn") }}</button>
        <button class="modal__btn edit" v-if="edit" @click="editNote">
         {{ $t("editbtn") }}
        </button>
        <button class="modal__btn edit" @click="sendNote" v-else>
          {{ $t ("addbtn") }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      text: "",
    };
  },
  methods: {
    close() {
      this.$emit("close");
    },
    sendNote() {
      if (this.text != "" && this.title != "") {
        let note = {
          title: this.title,
          text: this.text,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("sendNote", note);
      }
    },
    editNote() {
      if (this.text != "" && this.title != "") {
        let editedNote = {
          title: this.title,
          text: this.text,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("editNote", editedNote);
      }
    },
  },
  props: {
    edit: Boolean,
    note: Object,
  },
  created() {
    if (this.edit) {
      this.title = this.note.title
      this.text = this.note.text
    }
  },
};
</script>

<style lang="scss" scoped>
</style>