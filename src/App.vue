<template>
  <div class="main">
    <Header @changeLang="lang = $event" @search="search" :lang="lang"/>
    <Notes :notes="filterNotes" @delNote="delNote" @changeNote="changeNote" />
    <AddButton @click="openModal" />
    <Transition name="slide-modal">
      <Modal
       :note="editedNote" 
       @editNote="editNote" 
       v-if="modal" @close="close" 
       @sendNote="addNote" 
       :edit="edit" />
    </Transition>
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Notes from "@/components/Notes.vue";
import AddButton from "@/components/AddButton.vue";
import Modal from "@/components/Modal.vue";
let id = 1;
export default {
  components: {
    Header,
    Notes,
    AddButton,
    Modal,
  },
  data() {
    return {
      modal: false,
      edit: false,
      notes: [
        {
          id: id++,
          title: "Vue js",
          text: "Далеко-далеко за словесными горами в стране гласных и согласных живут, рыбные тексты. Страна то, своего предложения образ, журчит семантика буквоград обеспечивает необходимыми меня, рыбного всеми гор взгляд буквенных себя его рукопись? Ведущими!",
          date: new Date().toLocaleDateString(),
        },
        {
          id: id++,
          title: "React",
          text: "Далеко-далеко за словесными горами в стране гласных и согласных живут, рыбные тексты. Страна то, своего предложения образ, журчит семантика буквоград обеспечивает необходимыми меня, рыбного всеми гор взгляд буквенных себя его рукопись? Ведущими!",
          date: new Date().toLocaleDateString(),
        },
        {
          id: id++,
          title: "Angular",
          text: "Далеко-далеко за словесными горами в стране гласных и согласных живут, рыбные тексты. Страна то, своего предложения образ, журчит семантика буквоград обеспечивает необходимыми меня, рыбного всеми гор взгляд буквенных себя его рукопись? Ведущими!",
          date: new Date().toLocaleDateString(),
        },
      ],
      editedNote: null,
      filterNotes: null,
      lang: 'ru'
    };
  },
  methods: {
    openModal() {
      this.modal = true;
    },
    close() {
      this.edit = this.modal = false;
    },
    addNote(note) {
      note.id = id++;
      this.notes.push(note);
      this.close();
    },
    delNote(noteId) {
      this.notes.forEach((el, index) => {
        if (el.id == noteId) {
          this.notes.splice(index, 1);
        }
      });
    },
    editNote(note) {
      this.editedNote.title = note.title;
      this.editedNote.text = note.text;
      this.editedNote.date = note.date;
      this.notes.forEach((el, index) => {
        if (el.id == this.editedNote.id) {
          this.notes.splice(index, 1, this.editedNote);
        }
      });
      this.close()
    },
    changeNote(note) {
      this.modal = this.edit = true;
      this.editedNote = note;
    },
    search(value) {
      let notes = this.notes.filter(el=> el.title.toLowerCase().includes(value.toLowerCase()))
      this.filterNotes = notes
    }
  },
  watch: {
    notes: {
      handler(value) {
        localStorage.notes = JSON.stringify(value);
      },
      deep: true,
    },
    lang(value){
      localStorage.lang = value;
    }
  },
  created() {
    if (localStorage.notes) {
      let localNotes = JSON.parse(localStorage.notes);
      this.notes = localNotes;
      id = this.notes[this.notes.length - 1]
        ? this.notes[this.notes.length - 1].id + 1
        : 1;
    }
    this.filterNotes = this.notes;
    if (localStorage.lang) {
      this.lang = localStorage.lang
    }
  },
};
</script>

<style lang="scss" scoped></style>