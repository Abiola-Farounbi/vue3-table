<template>

  <div class="searchBar">
    <!-- Filter Search -->
      <div class="input-group mb-5">
        <input type="search" class="form-control" v-model='filterSearch' placeholder="Student's Name" aria-label="Recipient's username" aria-describedby="button-addon2">
        <button class="btn btn-success text-white" type="button" id="button-addon2"  @click="filterTable()">Search</button>
      </div>
  </div>

<table id="tableComponent" class="table table-bordered table-striped">
  <thead>
    <tr>
      <!-- loop through each value of the fields to get the table header -->
      <th  v-for="field in fields" :key='field' @click="sortTable(field)" > 
        {{field}} <i class="bi bi-sort-alpha-down" aria-label='Sort Icon'></i>
       </th>
    </tr>
  </thead>
  <tbody>
      <!-- Loop through the list get the each student data -->
      <tr v-for="item in sortedList" :key='item'>
      <td v-for="field in fields" :key='field'>{{item[field]}}</td>
    </tr>
  </tbody>
</table> 
</template>
<script>
import {computed,ref} from "vue";
export default {
  name: 'TableComponent',
  props:{
      studentData:{
          type: Array,
      },
      fields:{
          type: Array,
      }
  },
  
  setup(props) {
    
    let sort = ref(false);
    let updatedList =  ref([])
    
    
  
   
    // a function to sort the table
    const sortTable = (col) => {
      sort.value = true
      updatedList.value =  props.studentData 
       updatedList.value.sort(function(a, b) {
        if (a[col] > b[col]) {
          return 1;
        } else if (a[col] < b[col]) {
          return  -1;
        }
        return 0;
      })
      console.log(sortedList.value)
    }


      const sortedList = computed(() => {
        if (sort.value) {
         return updatedList.value
      }
      else{
         return props.studentData;
      }
      });

  return {sortedList, sortTable}
  }
 
}
</script>
<style scoped>
table th:hover {
        background:#f2f2f2;
      }
</style>