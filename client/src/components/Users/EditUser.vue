<template>
  <div>
    <div class="center bg-light">
      <h1>แก้ไขข้อมูลผู้ใช้งาน</h1>
      <div class="row">
        <div class="col-sm-12">
          <div class="card">
            <div class="card-body">
              <form v-on:submit.prevent="editUser">
                <p class="left">ชื่อ: <input class="form-control" type="text" v-model="user.name" /></p>
                <p class="left">นามสกุล: <input class="form-control" type="text" v-model="user.lastname" /></p>
                <p class="left">อีเมล: <input class="form-control" type="text" v-model="user.email" /></p>
                <p class="left">รหัสผ่าน: <input class="form-control" type="text" v-model="user.password" /></p>
                <p class="left">status: <input class="form-control" type="text" v-model="user.status" /></p>
                <p ><button class="btn btn-primary btn-warning" type="submit">แก้ไข</button></p>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";
export default {
  data() {
    return {
      user: {
        name: "",
        lastname: "",
        email: "",
        password: "",
        status: "",
      },
    };
  },
  methods: {
    async editUser() {
      try {
        await UsersService.put(this.user);
        this.$router.push({
          name: "MainAdmin",
        });
      } catch (err) {
        console.log(err);
      }
    },
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UsersService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
.center {
  text-align: center;
  padding: 3% 20%;
}
.left {
  text-align: left;
}
</style>