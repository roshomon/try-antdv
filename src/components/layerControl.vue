<template>
  <a-collapse activeKey="1">
    <a-collapse-panel key="1" header="电网">
      <a-row>
        <a-col :flex="1">
          <a-checkbox
            v-model:checked="checkAll"
            :indeterminate="indeterminate"
            @change="onCheckAllChange"
          >
            Check all
          </a-checkbox>
        </a-col>
        <a-col :flex="4">
          <a-checkbox-group v-model:value="checkedList" :options="plainOptions" />
        </a-col>
      </a-row>

      <br />

      <a-checkbox-group v-model:value="value">
        <a-row>
          <a-col :span="8">
            <a-checkbox value="A">A1111111</a-checkbox>
          </a-col>
          <a-col :span="8">
            <a-checkbox value="B">B1111</a-checkbox>
          </a-col>
          <a-col :span="8">
            <a-checkbox value="C">C1</a-checkbox>
          </a-col>
          <a-col :span="8">
            <a-checkbox value="D">D</a-checkbox>
          </a-col>
          <a-col :span="8">
            <a-checkbox value="E">E</a-checkbox>
          </a-col>
        </a-row>
      </a-checkbox-group>
    </a-collapse-panel>
  </a-collapse>
</template>
<script>
import { defineComponent, reactive, toRefs, watch } from "vue";
const plainOptions = ["Apple", "Pear", "Orange"];
export default defineComponent({
  setup() {
    const state = reactive({
      indeterminate: true,
      checkAll: false,
      checkedList: ["Apple", "Orange"],
    });

    const onCheckAllChange = (e) => {
      Object.assign(state, {
        checkedList: e.target.checked ? plainOptions : [],
        indeterminate: false,
      });
    };

    watch(
      () => state.checkedList,
      (val) => {
        state.indeterminate = !!val.length && val.length < plainOptions.length;
        state.checkAll = val.length === plainOptions.length;
      }
    );
    return { ...toRefs(state), plainOptions, onCheckAllChange };
  },
});
</script>
