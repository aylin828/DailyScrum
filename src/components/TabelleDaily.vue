<template>
  <div class="hello">
    <div id="add-table"> </div>
    <form target="1">

    <table class="eingabe" >
    <tr>
      <b-form-datepicker id="example-datepicker" v-model="date" class="mb-2"></b-form-datepicker> </tr>
    <tr>
    <td><label for = "gestern">Was habe ich gestern gemacht?</label></td>
     <td> <input v-model="doings" type ="text" placeholder="Geben Sie ein, was sie gemacht haben!"></td>
      <br>
    </tr>
     <tr> 
     <td><label for = "heute">Was habe ich heute vor?</label></td>
      <td><input v-model="todaydoings" type ="text" placeholder="Geben Sie ein was Sie heute vor haben!">
      <br></td></tr>

    <tr>  <td><label for = "probleme">Welche Probleme hatte ich?</label></td>
      <td><input v-model="problems" type ="text" placeholder="Geben Sie ein, welche Probleme es gab!"></td>
    </tr>
    </table>
    </form>
    <br>

    <div id="button">
    <div id="button_container_1">
        
        <button type="button" class="btn btn-primary" @click="addItem()">Hinzufügen</button>
    </div>
<br>
</div>
    <div id="Einsicht">
        <h3> Einsicht </h3>
        <table>
            <tr>
                <th> Datum: </th>
                <th> Was habe ich gestern gemacht? </th>
                <th>Was habe ich heute vor?</th>
                <th> Welche Probleme hatte ich? </th>
            </tr>
            
            <tr v-for="(row, id) in rowData" :key="row.id">
                <td> {{ row.date}} </td>
                <td> {{row.doings}} </td>
                <td>{{row.todaydoings}}</td>
                <td> {{row.problems}} </td>
                <td><button @click="deleteRow(id, row)">Lösche</button></td> 
            </tr>

        </table>

   </div>
   </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios, axios)
export default {
  
  
  name: 'TabelleDaily',
  props: {
    msg: String
  },
  data() {
  
    return {
      
      date: "",
      doings: "",
      todaydoings: "",
      problems: "",

      rowData: [
        
        { id: 1, date: " ", doings: " ", todaydoings: " ", problems: " "  },
        
      ]

    };  
  },
  
  methods: {
    addItem() {
            var ausgabe = {
                date: this.date,
                doings: this.doings,
                todaydoings: this.todaydoings,
                problems: this.problems
            };

            this.rowData.push(ausgabe)

            this.date = ''
            this.doings = ''
            this.todaydoings= ''
            this.problems = ''
        },
    deleteRow(id, row){
      var indx = this.rowData.indexOf(row);
      console.log(indx, row.id) ;
      if(indx > -1){
        this.rowData.splice(indx, 1);
      }

    }
  }
    
}

</script>



<style scoped>


table, td, th {
  height: 30px;
  border: 1px solid black;
  text-align: left;
}

table {
  width: 100%;
  border-collapse: collapse;
}
input {
  width: 60%;
}
b-form-datepicker{
  width: 60%;
}
.eingabe{
  border-style: none;
}
</style>