<script setup>
import { ref } from 'vue';

const openModal = ref(false);
const newNote = ref('');
const notes = ref([]);

const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    date: new Date(),
  });
  openModal.value = false;
  newNote.value = '';
};
</script>

<template>
  <!-- Modal component -->
  <div v-if="openModal" class="overlay">
    <div class="card w-50">
      <div class="card-body">
        <h3>Add note below</h3>
        <textarea
          v-model="newNote"
          class="form-control mb-3"
          placeholder="Leave a comment here"
          rows="5"
        />
        <button @click="addNote" class="btn-primary btn me-2">Save Note</button>
        <button @click="openModal = false" class="btn btn-outline-secondary">
          Cancel
        </button>
      </div>
    </div>
  </div>
  <!-- End Modal Component -->

  <main class="my-5 container">
    <div class="d-flex justify-content-between">
      <h1>Rapha Notes {{ openModal }}</h1>
      <button @click="openModal = true" class="btn-primary btn">
        New Note +
      </button>
    </div>
    <hr />

    <div class="row g-4">
      <!-- Card component -->
      <div v-for="note in notes" class="col-4">
        <div class="card card-body bg-light">
          <p class="card-text">{{ note.text }}</p>
          <p class="card-text">
            <small class="text-muted">{{
              note.date.toLocaleDateString('en-UK')
            }}</small>
          </p>
        </div>
      </div>
      <!-- End card component -->
    </div>
  </main>
</template>

<style scoped>
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}
</style>
