<template>
  <div class="container">
    <header>
      <h1>Notes App</h1>
    </header>
    <main>
      <Note
        v-for="(note, index) in notes"
        :key="index"
        :title="note.title"
        :body="note.body"
      />
      <div class="note">
        <form @submit="submitForm()">
          <input type="text" placeholder="Note Title" v-model="title" />
          <textarea placeholder="Note Body" v-model="body"></textarea>
          <input type="submit" value="Add Note" />
        </form>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Note from "./components/Note.vue";

type NoteType = {
  title: string;
  body: string;
};

@Component({
  components: {
    Note,
  },
})
export default class App extends Vue {
  notes: Array<NoteType> = [];
  title!: string;
  body?: string;

  constructor() {
    super();
    const data = localStorage.getItem("notes");
    if (data) this.notes = JSON.parse(data);
  }

  submitForm(): void {
    let note: NoteType = {
      title: this.title,
      body: this.body || "",
    };
    this.notes.push(note);
    localStorage.setItem("notes", JSON.stringify(this.notes));
  }
}
</script>

<style lang="scss">
body {
  height: 100%;
  width: 100%;
  margin: 0;
}

.container {
  width: 100%;
  height: auto;
  margin: 0;
  display: flex;
  flex-direction: column;

  header {
    display: flex;
    align-items: center;

    width: 100%;
    height: 56px;
    background-color: #4e78b8;
    color: white;

    h1 {
      margin-left: 6px;
    }
  }

  main {
    margin: 10px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    grid-gap: 1rem;
    align-items: center;

    .note {
      display: flex;
      flex-direction: column;

      padding: 10px;
      background-color: #a15fbb;
      border-radius: 5px;

      form {
        display: flex;
        flex-direction: column;

        textarea {
          resize: none;
        }
      }
    }
  }
}
</style>
