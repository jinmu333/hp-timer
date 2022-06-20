<template>
  <div class="dark">
    <el-row :gutter="20">
      <el-col :span="12">
        <el-form-item label="起始时间">
          <el-date-picker
            v-model="startDatetime"
            type="datetime"
            placeholder="起始时间"
          />
        </el-form-item>
      </el-col>
      <el-col :span="4"
        ><el-button type="primary" @click="getCurrentTime"
          >获取当前时间</el-button
        >
      </el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="12">
        <el-form-item label="起始树脂">
          <el-input v-model="startValue" />
        </el-form-item>
      </el-col>
      <el-col :span="4"></el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="12">
        <el-form-item label="期望时间">
          <el-date-picker
            v-model="expectDatetime"
            type="datetime"
            placeholder="期望时间"
          />
        </el-form-item>
      </el-col>
      <el-col :span="4"
        ><el-button type="primary" @click="computeValue">计算树脂</el-button>
      </el-col>
    </el-row>
    <el-row :gutter="20">
      <el-col :span="12">
        <el-form-item label="期望树脂">
          <el-input v-model="expectValue" />
        </el-form-item>
      </el-col>
      <el-col :span="4"
        ><el-button type="primary" @click="computeExpectDatetime"
          >计算时间</el-button
        ></el-col
      >
    </el-row>
  </div>
</template>

<script>
import { dayjs, ElMessageBox } from "element-plus";

export default {
  name: "TimerComponent",
  data() {
    return {
      startDatetime: new Date(),
      expectDatetime: new Date(),
      startValue: 0,
      expectValue: 160,
    };
  },
  methods: {
    getCurrentTime() {
      this.startDatetime = new Date();
      this.expectDatetime = new Date();
    },
    computeValue() {
      this.expectValue =
        parseInt(this.startValue) +
        parseInt((this.expectDatetime - this.startDatetime) / 1000 / 60 / 8);
      this.expectValue = this.expectValue > 160 ? 160 : this.expectValue;
      return ElMessageBox.alert(
        dayjs(this.expectDatetime).format("YYYY-MM-DD HH:mm:ss") +
          " 时, 树脂可恢复到" +
          this.expectValue,
        "提示",
        {
          confirmButtonText: "OK",
        }
      );
    },
    computeExpectDatetime() {
      this.expectDatetime = new Date(this.startDatetime);
      this.expectDatetime.setTime(
        this.startDatetime.getTime() +
          (this.expectValue - this.startValue) * 1000 * 60 * 8
      );
      return ElMessageBox.alert(
        dayjs(this.expectDatetime).format("YYYY-MM-DD HH:mm:ss") +
          " 时, 树脂可恢复到" +
          this.expectValue,
        "提示",
        {
          confirmButtonText: "OK",
        }
      );
    },
  },
};
</script>

<style>
.el-row {
  margin-bottom: 20px;
}
.el-row:last-child {
  margin-bottom: 0;
}
.el-col {
  border-radius: 4px;
}

.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
</style>
