<template>
  <div>
    <h2>I2C Readings</h2>
    <div class="table-container">
      <table class="custom-table">
        <colgroup>
          <col style="width: 50%" />
          <col style="width: 50%" />
        </colgroup>
        <thead>
          <tr>
            <th v-for="(header, index) in columnHeaders" :key="index">
              {{ header }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, rowIndex) in tableData" :key="rowIndex">
            <td>{{ customArray[rowIndex] }}</td>
            <td>{{ secondColumnArray[rowIndex] }}</td>
          </tr>
        </tbody>
      </table>
      <div class="button-container">
        <button class="update-button" @click="updateColumn2()">
          Update Readings
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PsuReadings',
  data() {
    return {
      numRows: 3,
      numColumns: 2,
      columnHeaders: ['PSU I2C Reading', 'Value'],
      customArray: ['Temperature', 'Vout', 'Vin'],
      secondColumnArray: [23, 12, 119],
      tableData: [],
      dp: 2, // decimal places
    };
  },
  created() {
    this.generateTableData();
  },
  methods: {
    generateTableData() {
      this.tableData = Array.from({ length: this.numRows }, () =>
        Array.from(
          { length: this.numColumns - 1 },
          (v, i) => `Row ${i + 1} Column ${i + 2}`
        )
      );
    },

    updateColumn2() {
      // Update the values in the second column
      let randomNum = parseFloat((Math.random() - 0.5).toFixed(this.dp));
      this.secondColumnArray = [
        33 + randomNum,
        12 + randomNum,
        120 + randomNum,
      ];
    },
  },
};
</script>

<style scoped>
.table-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.custom-table {
  width: 50%;
  border-collapse: collapse;
  margin: 20px;
}

.custom-table th,
.custom-table td {
  padding: 10px;
  text-align: left;
  border: 1px solid #ddd;
}

.custom-table th {
  background-color: #337ab7; /* Blue background for table header */
  color: #fff; /* White text color for table header */
  font-weight: bold;
}

.custom-table td {
  background-color: #d9edf7; /* Light blue background for table cells */
  color: #333; /* Dark gray text color for table cells */
}

.custom-table td:first-child {
  color: #337ab7; /* Blue text color for the first column */
}

.update-button {
  background-color: #337ab7; /* Blue background color for the button */
  color: #fff; /* White text color for the button */
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.button-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.update-button:hover {
  background-color: #23527c; /* Darker blue background color on button hover */
}
</style>
