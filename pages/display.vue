<template>
  <div class="body">
    <b-container fluid class="header">
      <b-row class="text-center">
        <b-col>
          <b-img
            rounded
            height="60px"
            alt="Rounded image"
            src="~assets/images/logo_SAKC.png"
          ></b-img
        ></b-col>
        <b-col cols="8">
          <h2 class="text-white mt-2">Queue Management System</h2></b-col
        >
        <b-col>3 of 3</b-col>
      </b-row>
    </b-container>
    <table
      id="example"
      class="table table-striped table-bordered"
      style="width: 100%"
    >
      <thead class="thead-dark">
        <tr>
          <th class="text-center" style="width:10%"><b-button size="lg">#</b-button></th>
          <th style="width:10%"
            class="text-center"
            v-for="(item, index) in itemsBay"
            :key="index"
          >
            <b-button
              block
              size="lg"
              :variant="getActiveQueue(item.is_queue)"
              >{{ item.bay_name }}</b-button
            >
          </th>
          <th class="text-center" style="width:10%">
            <b-button block size="lg" variant="primary">รับตั๋ว</b-button>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>
            <div class="text-center">
              <b-button class="mt-5" variant="info">
                Loading <b-badge variant="light">4</b-badge>
              </b-button>
            </div>
          </td>
          <td v-for="(item, index) in itemsLoading" :key="index">
            <div class="card bg-dark text-white" v-if="item.is_active">
              <div class="card-body" variant="primary">
                <h5 class="card-title">{{ item.truck_id }}</h5>
                <!-- <p class="card-text">{{ item.driver_name }}</p> -->
                <a href="#" block class="btn btn-light">{{ item.status }}</a>
              </div>
            </div>
          </td>

          <td>
            <div class="card bg-secondary text-white">
              <div class="card-body" variant="primary">
                <h5 class="card-title">75-7576</h5>
                <!-- <p class="card-text">นายมนัส บุญจำนง</p> -->
                <a href="#" class="btn btn-info">เข้ารับตั๋ว</a>
              </div>
            </div>
          </td>
        </tr>
      </tbody>
      <tbody>
        <tr>
          <td rowspan="8">
            <div class="text-center">
              <b-button block variant="outline-primary"
                >Standby <b-badge variant="danger">10</b-badge></b-button
              >
            </div>
          </td>
        </tr>
        <tr>
          <td  v-for="(item, index) in itemsBay" :key="index">
              <div 
                v-for="(itemBay, idxItemBay) in loadItemStandBy(item.bay_no)"
                :key="idxItemBay" class="mt-2"
              >
                  <div  :class="getActiveColor(itemBay.call_queue)"  v-if="itemBay !== null">
                    <div class="card-body" variant="primary" >
                      <h5 class="card-title">{{ itemBay.truck_id }}</h5>
                      <!-- <p class="card-text">{{ item.driver_name }}</p> -->
                      <a href="#" block class="btn btn-primary active">{{ itemBay.status }}</a>
                    </div>
                  </div>
                </div>
          </td>
        </tr>
      </tbody>
    </table>
    <!-- Footer -->
  <footer class="text-center text-white" style="background-color: #0a4275;">
    <!-- Grid container -->
    <div class="container p-4 pb-0">
      <!-- Section: CTA -->
      <!-- Section: CTA -->
    </div>
    <!-- Grid container -->

    <!-- Copyright -->
    <div class="text-center p-3" style="background-color: rgba(0, 0, 0, 0.2);">
      © 2023 Copyright:
      <a class="text-white" href="https://mdbootstrap.com/">G-innovation</a>
    </div>
    <!-- Copyright -->
  </footer>
  <!-- Footer -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      current_date_time: '',
      itemsBay: [
        { bay_no: 1, bay_name: 'BAY 1', is_queue: true },
        { bay_no: 2, bay_name: 'BAY 2', is_queue: false },
        { bay_no: 3, bay_name: 'BAY 3', is_queue: true },
        { bay_no: 4, bay_name: 'BAY 4', is_queue: false },
        { bay_no: 5, bay_name: 'BAY 5', is_queue: true },
        { bay_no: 6, bay_name: 'BAY 6', is_queue: true },
        { bay_no: 7, bay_name: 'BAY 7', is_queue: true },
      ],
      itemsLoading: [
        {
          load_no: 1,
          truck_id: '75-0001',
          is_active: true,
          status: 'กำลังเติม',
          driver_name: 'นายชวลิต อรุณไพร',
        },
        {
          load_no: 2,
          truck_id: '75-0002',
          is_active: false,
          status: 'กำลังเติม',
          driver_name: 'นายนิพล โพสฤทธ',
        },
        {
          load_no: 3,
          truck_id: '75-0003',
          is_active: true,
          status: 'เติมเสร็จ',
          driver_name: 'นายสวง สาระศาลิน',
        },
        {
          load_no: 4,
          truck_id: '75-0004',
          is_active: true,
          status: 'กำลังเติม',
          driver_name: 'นายสมบัติ นามฝาง',
        },
        {
          load_no: 5,
          truck_id: '75-0005',
          is_active: false,
          status: 'เติมเสร็จ',
          driver_name: 'นายปรีชา  คเณรุพันธ์',
        },
        {
          load_no: 6,
          truck_id: '75-0006',
          is_active: true,
          status: 'กำลังเติม',
          driver_name: 'นายชวลิต อรุณไพร',
        },
        {
          load_no: 7,
          truck_id: '75-0007',
          is_active: true,
          status: 'เติมเสร็จ',
          driver_name: 'นายศุภกรณ์ชัย ศรลัมภ์',
        },
      ],
      itemsStandby: [
        {
          bay_no: 1,
          load_no: 1,
          truck_id: '75-0001',
          is_active: true,
          status: 'เข้าเติม',
          driver_name: 'นายชวลิต',
          call_queue: true,
        },
        {
          bay_no: 1,
          load_no: 2,
          truck_id: '75-0002',
          is_active: false,
          status: 'กำลังเติม',
          driver_name: 'นายนิพล',
          call_queue: false,
        },
        {
          bay_no: 1,
          truck_id: '75-0003',
          is_active: true,
          status: 'เติมเสร็จ',
          driver_name: 'นายสวง',
          call_queue: false,
        },
        {
          bay_no: 3,
          load_no: 4,
          truck_id: '75-0004',
          is_active: true,
          status: 'กำลังเติม',
          driver_name: 'นายสมบัติ',
          call_queue: false,
        },
        {
          bay_no: 3,
          load_no: 5,
          truck_id: '75-0005',
          is_active: false,
          status: 'เติมเสร็จ',
          driver_name: 'นายปรีชา',
          call_queue: false,
        },
        {
          bay_no: 7,
          load_no: 6,
          truck_id: '75-0006',
          is_active: true,
          status: 'กำลังเติม',
          driver_name: 'นายชวลิต',
          call_queue: false,
        },
        {
          bay_no: 7,
          load_no: 7,
          truck_id: '75-0007',
          is_active: true,
          status: 'เติมเสร็จ',
          driver_name: 'นายศุภกรณ์ชัย',
          call_queue: false,
        },
      ],
    }
  },
  mounted() {
    //this.showLocalTime();
  },
  methods: {
    showLocalTime() {
      setInterval(function () {
        let date = new Date()
        this.current_date_time = date.toLocaleString()
        console.log(this.current_date_time)
      }, 1000)
    },
    getActiveQueue(is_queue) {
      return is_queue ? 'success' : 'danger'
    },
    getActiveColor(value){
      if (value) {
          return ['card bg-danger', 'text-white','btn']
        } else {
          return ['card bg-warning', 'text-white','btn']
        }
    },
    loadItemStandBy(bay_no) {
      const check = this.itemsStandby.filter((item) => item.bay_no === bay_no)
      if (check) {
        return this.itemsStandby.filter((item) => item.bay_no === bay_no)
      } else {
        return null
      }
    },
  },
}
</script>
<style scoped>
.header {
  background: rgb(2, 0, 36);
  background: linear-gradient(
    90deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(0, 74, 152, 1) 54%,
    rgba(0, 212, 255, 1) 100%
  );
}
.body {
  font-family: 'Noto Serif Thai', serif;
}
</style>
