<template>
  <div class="p-4">
    <BasicTable @register="registerTable">
      <template #action>
        <TableAction
          :actions="[
            {
              label: '删除',
              onClick: handleDelete,
            },
          ]"
          :dropDownActions="[
            {
              label: '启用',
              onClick: handleOpen,
            },
          ]"
        />
      </template>
    </BasicTable>
  </div>
</template>
<script lang="ts">
  import { defineComponent } from 'vue';
  import { BasicTable, useTable, BasicColumn, TableAction } from '/@/components/Table';

  import { demoListApi } from '/@/api/demo/table';
  const columns: BasicColumn[] = [
    {
      title: 'ID',
      dataIndex: 'id',
      fixed: 'left',
      width: 280,
    },
    {
      title: '姓名',
      dataIndex: 'name',
      width: 260,
    },
    {
      title: '地址',
      dataIndex: 'address',
      width: 260,
    },
    {
      title: '编号',
      dataIndex: 'no',
      width: 300,
    },
    {
      title: '开始时间',
      width: 200,
      dataIndex: 'beginTime',
    },
    {
      title: '结束时间',
      dataIndex: 'endTime',
      width: 200,
    },
  ];
  export default defineComponent({
    components: { BasicTable, TableAction },
    setup() {
      const [registerTable] = useTable({
        title: 'TableAction组件及固定列示例',
        api: demoListApi,
        columns: columns,
        rowSelection: { type: 'radio' },
        actionColumn: {
          width: 160,
          title: 'Action',
          dataIndex: 'action',
          slots: { customRender: 'action' },
        },
      });
      function handleDelete() {
        console.log('点击了删除');
      }
      function handleOpen() {
        console.log('点击了启用');
      }
      return {
        registerTable,
        handleDelete,
        handleOpen,
      };
    },
  });
</script>
