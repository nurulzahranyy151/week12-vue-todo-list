<script setup>
import { ref, reactive, onMounted, onUnmounted } from "vue"

// Materi ref() To Do List 
const tasks = ref([])
const newTask = ref('')

// Materi ref() Tambah task
function addTask() {
  if (newTask.value.trim() !== '') {
    tasks.value.push({ text: newTask.value.trim() })
    newTask.value = ''
  }
}

// Materi ref() Hapus task
function deleteTask(index) {
  tasks.value.splice(index, 1)
}

// Materi ref() Counter 
const count = ref(0)
const increment = () => count.value++
const decrement = () => count.value--
const reset = () => count.value = 0

// Materi reactive() User Profile
const user = reactive({
  name: "Nurul Qalbi Zahrani",
  age: 21,
  address: { city: "Jakarta", country: "Indonesia" }
})
const newCity = ref('')
const updateCity = () => {
  if(newCity.value.trim() !== ''){
    user.address.city = newCity.value.trim()
    newCity.value = ''
  }
}

// Materi Conditional Rendering 
const isLoggedIn = ref(false)
const userRole = ref("admin")
const catatan = ref("")

// Materi Lifecycle Hooks Timer
const seconds = ref(0)
let interval = null
onMounted(() => {
  interval = setInterval(() => { seconds.value++ }, 1000)
})
onUnmounted(() => {
  if(interval) clearInterval(interval)
})
</script>

<template>
  <div class="app">

    <!-- Login / Logout -->
    <div class="card login-card">
      <div><h1>Hi :>  </h1></div>
        <button v-if="!isLoggedIn" @click="isLoggedIn = true">Login</button>
        <button v-else @click="isLoggedIn = false">Logout</button>
    </div>

    <!-- User Profile -->
    <section v-if="userRole === 'admin' && isLoggedIn" class="card profile-card">
      <h1>Selamat Datang Kembali, {{ user.name }}</h1>
      <p>Umur: {{ user.age }} Tahun</p>
      <p>Kota: {{ user.address.city }}</p>
      <form @submit.prevent="updateCity">
        <input type="text" v-model="newCity" placeholder="Masukkan Kota Baru"/>
        <button type="submit">Ubah Kota</button>
      </form>
    </section>

     <!-- Timer -->
    <section v-if="isLoggedIn" class="card timer-card">
      <h3>Timer: {{ seconds }} detik</h3>
      <p>Belajar dengan Pomodoro!! :></p>
    </section>

    <!-- To Do List -->
    <section v-if="isLoggedIn" class="card todo-card">
      <h1>To Do List</h1>
      <form @submit.prevent="addTask">
        <input type="text" v-model="newTask" placeholder="Masukkan Tugas Baru"/>
        <button type="submit">Tambah ke List</button>
      </form>

      <ul v-if="tasks.length > 0">
        <li v-for="(task, index) in tasks" :key="index" class="todo-item">
          <label>
            <span :class="{ done: task.done }">{{ task.text }}</span>
          </label>
          <button @click="deleteTask(index)" class="delete-btn">Hapus</button>
        </li>
      </ul>
      <p v-else>Tidak ada tugas</p>
    </section>

    <!-- Counter -->
    <section v-if="isLoggedIn" class="card counter-card">
      <h1>Batas Pengerjaan (Hari)</h1>
      <p class="count">{{ count }}</p>
      <div class="counter-buttons">
        <button @click="increment">+ Tambah Hari</button>
        <button @click="decrement">- Kurang Hari</button>
        <button @click="reset">Reset</button>
      </div>
    </section>

    <!-- Catatan -->
    <section v-if="isLoggedIn" class="card notes-card">
      <label>Catatan:</label>
      <textarea v-model="catatan" rows="4" placeholder="Tulis Catatan..."></textarea>
    </section>
  </div>
</template>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  justify-content: center; 
  align-items: center;     
  min-height: 100vh;       
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #333;
  padding: 20px;
  box-sizing: border-box;
}

.card {
  background-color: #fdfdfd;
  border: 1px solid #ddd;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.05);
  transition: transform 0.1s ease;
}
.card:hover {
  transform: translateY(-2px);
}

.login-card {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.login-card .login-content h1 {
  margin-bottom: 15px;
}

h1,h2,h3 {
  margin-bottom: 10px;
  color: #2c3e50;
}

input[type="text"], textarea {
  width: 70%;
  padding: 10px;
  margin-right: 5px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 14px;
}
textarea { resize: vertical; }

button {
  padding: 10px 15px;
  margin-top: 5px;
  border: none;
  border-radius: 8px;
  background-color: #3498db;
  color: white;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s ease;
}
button:hover {
  background-color: #2980b9;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 10px;
}
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 12px;
  background-color: #f7f9fb;
  border-radius: 6px;
  margin-bottom: 8px;
  transition: transform 0.1s;
}
.todo-item:hover { transform: translateX(3px); }
.delete-btn { background-color: #e74c3c; }
.delete-btn:hover { background-color: #c0392b; }

.counter-buttons button { margin-right: 10px; }
.count { font-size: 24px; font-weight: bold; }

label { font-weight: 500; }
</style>
