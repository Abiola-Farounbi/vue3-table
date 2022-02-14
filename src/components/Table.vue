<template>
   <table id="tableComponent" class="table table-bordered table-striped">
  <thead>
    <tr>
      <!-- loop through each value of the column property to get the table header -->
      <th  v-for="col in columns" :key='col' @click="sortTable(col)" > {{col}} <i class="bi bi-sort-alpha-down"></i> </th>
    </tr>
  </thead>
  <tbody>
      <!-- Loop through the list get the each value -->
      <tr v-for="studentRow in sortedList" :key='studentRow'>
      <td v-for="col in columns" :key='studentRow[col]'>{{studentRow[col]}}</td>
    </tr>
  </tbody>
</table> 
</template>
<script>
import {computed} from "vue";

export default {
  name: 'TableComponent',
  props:{
      studentData:{
          type: Array,
      }
  },
  
  setup(props) {
    
    let sort = false;
    let updatedList =  []
    
    // The list of values
     const sortedList = computed(() => {
        if (sort) {
         return updatedList
      }
      else{
         return props.studentData;
      }
      });

    const columns = computed(() => {
        if (sortedList.value.length == 0) {
          return [];
      }
      return Object.keys(sortedList.value[0])
      });

   

    // a function to sort the table
    const sortTable = (col) => {
      sort =true
      updatedList =  props.studentData 
       updatedList.sort(function(a, b) {
        if (a[col] > b[col]) {
          return 1;
        } else if (a[col] < b[col]) {
          return  -1;
        }
        return 0;
      })
    }



  return { columns,sortedList, sortTable}
  }
 
}
</script>
<style scoped>
table th:hover {
        background:#f2f2f2;
      }
</style>