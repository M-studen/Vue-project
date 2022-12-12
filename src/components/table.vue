<script setup>
import { ElNotification } from "element-plus";
import { computed, reactive, watch, watchEffect } from "vue";
let computer = reactive([
  { id: 1, name: "Z690主板", price: "1999", brand: "华硕", number: 1 },
  { id: 2, name: "DDR5内存条", price: "299", brand: "芝奇", number: 4 },
  { id: 3, name: "I9-12900k", price: "1999", brand: "因特尔", number: 1 },
  { id: 4, name: "RTX3090ti", price: "10999", brand: "华硕", number: 1 },
  { id: 5, name: "三星980pro", price: "1499", brand: "三星", number: 3 },
]);

function ButtonAddClick(object) {
  if (object.number != 99) {
    object.number++;
    return 1;
  } else return 0;
}
function ButtonRedClick(object) {
  if (object.number - 1) {
    object.number--;
    return 1;
  } else return 0;
}
function ButtonDelClick(index) {
  computer.splice(index, 1);
  return 1;
}

function AddSuccess(f) {
  if (f) {
    ElNotification({
      title: "添加成功",
      message: "添加配件成功",
      type: "success",
    });
  } else {
    ElNotification({
      title: "添加失败",
      message: "已达到数据上限",
      type: "error",
    });
  }
}

function RedSuccess(f) {
  if (f) {
    ElNotification({
      title: "减除成功",
      message: "减除配件成功",
      type: "success",
    });
  } else {
    ElNotification({
      title: "减除失败",
      message: "必须保留至少一个配件",
      type: "error",
    });
  }
}
function DelSuccess(f) {
  if (f) {
    ElNotification({
      title: "删除成功",
      message: "删除配件成功",
      type: "success",
    });
  } else {
    ElNotification({
      title: "删除失败",
      message: "这可能是系统错误",
      type: "error",
    });
  }
}
const AllPrice = computed(() => {
  let allpric = 0;
  computer.forEach((element) => {
    let price = element.price * element.number;
    allpric += price;
  });
  return allpric;
});

// watch(computer, (newVal, oldVal) => {
//   console.log(oldVal, "==>", newVal);
// },{
//   deep:true,
//   immediate:true,
//   flush:'sync'
// });
watchEffect(() => {
  console.log(computer);
});
</script>

<template>
  <!-- <mytitle></mytitle>
  <mytable></mytable> -->
  <!-- <table border id="table-1">
    <thead>
      <th>名称</th>
      <th>价格</th>
      <th>品牌</th>
      <th>数量</th>
      <th>操作</th>
      <td>总价:{{ AllPrice }}</td>
    </thead>
    <tbody :key="parts.id" v-for="(parts, index) in computer">
      <td>{{ parts.name }}</td>
      <td>{{ parts.price }}</td>
      <td>{{ parts.brand }}</td>
      <td>
        {{ parts.number }}
      </td>
      <td>
        <button @click="ButtonAddClick(parts)">+</button>
        <button @click="ButtonRedClick(parts)">-</button>
        <button @click="ButtonDelClick(index)">Del</button>
      </td>
    </tbody>
  </table> -->
  <el-table :data="computer" style="width: 100%">
    <el-table-column prop="name" label="名称"></el-table-column>
    <el-table-column prop="price" label="价格"></el-table-column>
    <el-table-column prop="brand" label="品牌"></el-table-column>
    <el-table-column prop="number" label="数量"></el-table-column>
    <el-table-column label="操作">
      <template v-slot="scope">
        <el-button
          link
          type="primary"
          size="small"
          @click="
            () => {
              let f = ButtonAddClick(scope.row);
              AddSuccess(f);
            }
          ">
          <el-icon><Plus /></el-icon>
        </el-button>
        <el-button
          link
          type="primary"
          size="small"
          @click="
            () => {
              let f = ButtonRedClick(scope.row);
              RedSuccess(f);
            }
          ">
          <el-icon><Minus /></el-icon>
        </el-button>
        <el-button
          link
          type="primary"
          size="small"
          @click="
            () => {
              let f = ButtonDelClick(scope.$index);
              DelSuccess(f);
            }
          ">
          <el-icon><Delete /></el-icon>
        </el-button>
      </template>
    </el-table-column>
    <el-table-column label="总价" height="100%">{{ AllPrice }}</el-table-column>
  </el-table>
</template>

<style scoped>
/* Border styles
#table-1 thead,
#table-1 tr {
  border-top-width: 1px;
  border-top-style: solid;
  border-top-color: rgb(230, 189, 189);
}
#table-1 {
  border-bottom-width: 1px;
  border-bottom-style: solid;
  border-bottom-color: rgb(230, 189, 189);
  width: 800px;
}

/* Padding and font style */
/* #table-1 td,
#table-1 th {
  padding: 5px 10px;
  font-size: 12px;
  font-family: Verdana;
  color: rgb(177, 106, 104);
}

/* Alternating background colors */
/* #table-1 tr:nth-child(even) {
  background: rgb(238, 211, 210);
}
#table-1 tr:nth-child(odd) {
  background: #fff;
} */
/* button {
  display: inline-block;
  padding: 15px 25px;
  font-size: 12px;
  cursor: pointer;
  text-align: center;
  text-decoration: none;
  outline: none;
  color: #fff;
  background-color: #3192c9;
  border: none;
  border-radius: 15px;
  box-shadow: 0 3px #999;
  margin: 2px;
} */

/* button:hover {
  background-color: #3192c9;
}

button:active {
  background-color: #3192c9;
  box-shadow: 0 5px #666;
  transform: translateY(4px);
} */
</style>
