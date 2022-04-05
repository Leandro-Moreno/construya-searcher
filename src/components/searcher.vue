<template>
  <div class="card">
    <div class="card--header">
      <h1>Ingresa el nombre de la ferretería en la que vas a realizar tu compra.</h1>
    </div>
    <div class="card--content">
      <div class="input-group">
        <div class="selected" v-if="selected.name.length >0">
          <span>{{selected.name}}</span>
          <div class="close" @click="clearSelected"><i class="bx bxs-x-circle"></i></div>
        </div>
        <input class="form-control"
               placeholder="Nombre de la ferretería"
               type="text"
               v-model="searchQuery"
               @on-keyup="search"
               @keyup="search"
        >
        <div class="input-group-append">
          <button
              class="btn btn-squared btn-secondary"
                  type="button"
          @click="search"
          >
            <i class="bx bx-search"></i>
          </button>
        </div>
        <div class="search-results" v-if="resultsActive">
          <div v-for="(result, index) in searchActive" ref="result.id" class="result" @click="select(result.id, result.name)">
          <span
              v-if="index<4"
              ref="index"

          >{{ result.name }}</span>
          </div>
        </div>
      </div>

    </div>
    <div class="btn btn-primary">
      Continuar
    </div>
  </div>
</template>
<script>
import Papa from 'papaparse';

export default {
  name: 'searcher',
  data() {
    return {
      data: [],
      searchActive: [],
      searchQuery: '',
      selected: {
        name: '',
        id: '',
      },
      resultsActive: false,
    }
  },
  watch: {
    searchQuery: function(newValue) {
      if (newValue.length ==0) {
        this.resultsActive = false;
      }
      console.log("watch:"+newValue);
    },
  },
  methods: {
    importData() {
      Papa.parse('https://docs.google.com/spreadsheets/d/e/2PACX-1vQqFlrGirtl9hrlZ_YLzQZVWiO4q0aDNz80dPqoyhsMYKa3QnRpULZQyOOOardYr9V-az_GF2zivIyA/pub?output=csv', {
        download: true,
        header: true,
        complete: function (results) {
          this.data = results.data;
          this.searchActive = this.data;
        }.bind(this)
      });
    },
    clearSelected() {
      this.selected.name = '';
      this.selected.id = '';
      this.searchActive = this.data;
    },
    select(id, name) {
      this.searchQuery = '';
      this.resultsActive = false;
      this.selected.id = id;
      this.selected.name = name;
    },
    search() {
      //takes query String to search in data Array that contains object with name and id
      //returns array of objects that match the query
      console.log("search:"+this.searchQuery);
      if(this.searchQuery.length>0){
        this.resultsActive = true;
      }
      this.searchActive = this.data;
      //takes this.searchQuery and searches in this.data Object to return an array of objects that match the query
      this.searchActive = this.searchActive.filter(function (item) {
        return item.name.toLowerCase().includes(this.searchQuery.toLowerCase());
      }.bind(this));


    }
  },
  mounted() {
    this.importData();
  }
}

</script>
<style lang="scss">
.selected{
  position: absolute;
  top: 4px;
  display: block;
  background: #f9f9f9;
  z-index: 999;
  padding: 3px 24px;
  font-size: 15px;
  width: 68%;
  left: 10px;
  border-radius: 5px;
  border: 1px solid grey;
}
.close{
  width: 26px;
  height: 100%;
  position: absolute;
  right: 1px;
  top: 0;
  display: grid;
  align-content: center;
  background-color: #fff;
  cursor: pointer;
}
.search-results{
  top: 32px !important;
  border-radius: 0.6rem !important;
  display: block !important;
  width: 100% !important;
  padding: 0.5rem !important;
  position: absolute !important;
  z-index: 128 !important;
  background-color: #fff;
  box-shadow: 0 8px 17px 0 rgb(55 55 55 / 20%), 0 6px 20px 0 rgb(125 125 125 / 19%);
}
.result{
  padding: 3px 5px;
  background-color: white;
  cursor: pointer;
  &:hover{
    background-color: #2c3e50;
    color: white;
  }
}
.input-group {
  position: relative;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-wrap: nowrap;
  flex-wrap: nowrap;
  -ms-flex-align: stretch;
  align-items: stretch;
  width: 100%;

  &-append {
    display: flex;
    margin-left: -1px;



      &-secondary {
        color: #fff;
        background-color: #ced4da;
        border-color: #ced4da;
        border-radius: 0 5px 5px 0;
      }
    }
  }

.btn {
  cursor: pointer;
  position: relative;
  z-index: 2;
  border-radius: 0;
  border-top-right-radius: -1px;
  border-bottom-right-radius: -1px;

  &:hover {
    z-index: 3;
  }

  &-primary {
    background-color: #00356d;
    color: #cfe103;
    font-weight: 700;
    WIDTH: 100%;
  }
}
.form-control {
  position: relative;
  -ms-flex: 1 1 auto;
  flex: 1 1 auto;
  width: 1%;
  margin-bottom: 0;
  display: block;
  width: 100%;
  height: calc(2.25rem + 2px);
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  color: #495057;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
  transition: border-color .15s ease-in-out, box-shadow .15s ease-in-out;
}

.card {
  //background-color: rgb(249, 249, 249);
  box-shadow: 0 8px 17px 0 rgb(55 55 55 / 20%), 0 6px 20px 0 rgb(125 125 125 / 19%);
  position: relative;
  margin: 10px 0 20px 0;
  border-radius: 8px;
  background-color: white;
  padding: 25px;
  &--header {
    padding: 20px;

  }

  &--content {
    border-radius: 0 0 2px 2px;
    padding: 20px;
  }
}
</style>