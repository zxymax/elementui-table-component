<template>
  <el-select v-model="value" placeholder="请选择" @change="changeValue">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
</template>
<script>
  export default {
    props: ['myOptions'],
    data() {
      return {
        options: [],
        value: ''
      }
    },
    methods: {
      changeValue(val) {
        // console.log(val);
        let obj = {};
        obj = this.options.find((item)=>{
            return item.value === val;
        });
        console.log(obj.label);
      }
    },
    mounted() {
      this.options = this.myOptions.options
      this.value = this.myOptions.defaultV

      console.log( this.myOptions.options)

    }

  }
</script>