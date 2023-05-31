<template>
  <div>
    <DxDataGrid
      :data-source="employees"
      :show-borders="true"
      :hover-state-enabled="true"

      :allow-column-resizing="true"
      :word-wrap-enabled="true"
      :show-row-lines="true"
      :row-alternation-enabled="false"
      :focused-row-enabled="false"
      key-expr="ID"
      @selection-changed="onSelectionChanged"
    >
      <DxSelection
        mode="single"
      />
      <DxColumn
        :width="160"
        data-field="Prefix"
        caption="Системное наименование объекта"
      />
      <DxColumn 
      :width="160"
      data-field="FirstName"
      caption="Наименование объекта"
      />
      <DxColumn
      :width="160" 
      data-field="LastName"
      />
      <DxColumn
        :width="160"
        data-field="Positio"
      />
      <DxColumn
        data-field="BirthDate"
        data-type="date"
        caption="Полное наименование поля"
        :width="160"
      />

    </DxDataGrid>
    <div
      v-if="showEmployeeInfo"
      id="employee-info"
    >
    </div>
  </div>
</template>
<script>
import { DxDataGrid, DxColumn, DxSelection } from 'devextreme-vue/data-grid';
import { employees } from './data.js';

export default {
  components: {
    DxDataGrid,
    DxColumn,
    DxSelection,
  },
  data() {
    return {
      showEmployeeInfo: false,
      selectedRowNotes: '',
      selectedRowPicture: '',
      employees,
    };
  },
  methods: {
    onSelectionChanged({ selectedRowsData }) {
      const data = selectedRowsData[0];

      this.showEmployeeInfo = !!data;
      this.selectedRowNotes = data && data.Notes;
      this.selectedRowPicture = data && data.Picture;
    },
  },
};
</script>
<style scoped>
#employee-info .employee-photo {
  height: 100px;
  float: left;
  padding: 20px;
}

#employee-info .employee-notes {
  padding-top: 20px;
  text-align: justify;
}

.dark #employee-info .employee-notes {
  color: rgb(181, 181, 181);
}
</style>
