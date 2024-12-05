<template>
<div>
  <table class="table">
    <tr>
      <th>Asset Name</th>
      <th>Department</th>
    </tr>
    <tr>
      <td>Printer</td>
      <td>HR</td>
    </tr>
      <tr>
      <td>Monitor</td>
      <td>IT</td>
    </tr>
    <tr>
      <td>Barcode Scanner</td>
      <td>Account</td>
    </tr>
  </table>  
  <button class="download-btn" @click="downloadCSV">
    DOWNLOAD
  </button>
</div>
</template>

<script>
export default {
  name: 'HelloWorld1',
  props: {
    msg: String
  },
  methods: {
    downloadCSV() {
      // Get table data
      const table = document.querySelector('table');
      const rows = table.querySelectorAll('tr');
      
      let csv = [];
      rows.forEach(row => {
        const cells = row.querySelectorAll('th, td');
        const rowData = Array.from(cells).map(cell => {
          return `"${cell.textContent.replace(/"/g, '""')}"`;
        });
        csv.push(rowData.join(','));
      });
      const csvContent = csv.join('\n');
      
      const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
      const link = document.createElement('a');
      const url = URL.createObjectURL(blob);
      link.setAttribute('href', url);
      link.setAttribute('download', 'table_data.csv');
      link.style.visibility = 'hidden';
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
.download-btn {
  display: block;
  margin-top: 20px;
}


/* Remove bold font from header cells */
th {
  font-weight: normal;
}
</style>