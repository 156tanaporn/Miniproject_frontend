<template lang="">
  <div>
    <ul>
        <li><a class="active" href="#home">Home</a></li>
        <li><a href="#product">Products</a></li>
        <li><a href="#review">Reviews</a></li>
        <li><a href="#login">Login</a></li>
    </ul>
  </div>
</template>

<script>
export default {

}
</script>

<style>
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
    background-color: rgb(86, 174, 212);
}
li {
  float: right; /* จัดให้รายการลิสต์แสดงติดกันแนวนอน */
}
li a {
  display: block; /* ทำให้ลิงค์เต็มพื้นที่ของรายการ */
  color: white; /* สีข้อความ */
  text-align: center; /* จัดให้ข้อความแนวตรงกลาง */
  padding: 14px 16px; /* ระยะห่างรอบข้อความของลิงค์ */
  text-decoration: none; /* ไม่มีขีดเส้นใต้ข้อความลิงค์ */
}
/* กำหนดสไตล์ลิงค์เมื่อโฮเวอร์เมาส์ไฟล์ */
li a:hover {
  background-color: #555; /* เมื่อโฮเวอร์เมาส์ไฟล์จะเปลี่ยนสีพื้นหลัง */
}

</style>
