<script setup>
import { ref, onMounted } from "vue";

//ตัวแปรเก็บข้อมูล

const myName = ref("");
const studentID = "664259009";

//ดึงข้อมูลจาก json
const fetchData = async () => {
    try {
        const response = await fetch ("/data.json"); // โหลดไฟล์ JSON 
        const data = await response.json();

        //ค้นหาชื่อเราด้วย ID

        const student = data.students.find((s) => s.id ===studentID);

        if (student) {
            myName.value = student.name;
        }
    } catch (error) {
        console.error ("ไม่ได้จ้าสาว",error);
    }
};

// โหลดข้อมูลตอน Component ทำงาน
onMounted(fetchData);
</script>

<template>
  <div>
    <h1>สวัสดี! 👋</h1>
    <h2 v-if="myName">ชื่อของคุณคือ: {{ myName }}</h2>
    <h2 v-else>กำลังโหลดข้อมูล...</h2>
  </div>
</template>

<style scoped>
h1 {
  color: #42b983;
}
</style>