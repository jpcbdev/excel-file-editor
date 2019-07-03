<template>
  <div class="hello">
    <h5>{{title}}</h5>
    <table>
      <thead>
        <tr>
          <!-- <th>Name</th>
          <th>Item Name</th>
          <th>Item Price</th>-->
          <th v-for="column in columns" :key="column.id">{{column}}</th>
        </tr>
      </thead>

      <tbody>
        <tr>
          <td v-for="item in info" :key="item.id">{{item}}</td>

          <!-- <td>Alvin</td> -->
        </tr>
      </tbody>
    </table>

    <input id="input" type="file" accept=".xls, .xlsx" />
  </div>
</template>

<script>
import readXlsxFile from "read-excel-file";

export default {
  name: "HelloWorld",
  data() {
    return {
      title: "",
      columns: [],
      info: []
    };
  },
  props: {
    msg: String
  },
  mounted() {
    const input = document.getElementById("input");

    input.addEventListener("change", () => {
      readXlsxFile(input.files[0]).then(rows => {
        this.title = rows[0][0];
        this.columns = rows[1];
        this.info = Object.values(rows[2]);

        // console.log(Object.values(rows[2]));
        // rows.map((row, index) => {
        //   if (row[index] >= 2) {
        //     console.log(row);
        //   }
        // });
      });
    });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
th {
  font-size: 0.7em;
}
</style>
