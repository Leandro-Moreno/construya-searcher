<template>
  <div>
    <div class="card">
    <div class="card--header">
      <h1>Realiza tu solicitud de crédito</h1>
      <p>Ingresa el nombre o ciudad de la ferretería en la que vas a realizar tu compra.</p>
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
               v-on:input="search"
               ref="searchQuery"
        >
        <div class="input-group-append"
             v-if="mobile"
        >
          <button
              class="btn btn-squared btn-secondary"
                  type="button"
          @click="search"
          >
            <i class="bx bx-search"></i>
          </button>

        </div>
        <div class="btn btn-primary" @click="sendToPage">
          Solicitar
        </div>
        <div class="search-results" v-if="resultsActive">
          <div v-for="(result, index) in searchActive.slice(0, 6)" ref="result.id" class="result" @click="select(result.id, result.name, result.ciudad)">
          <span
              ref="index"

          >{{ result.name }} - {{result.ciudad}}</span>
          </div>
        </div>
      </div>
      {{selected.ciudad}}
    </div>
      <p>Para realizar tu solicitud es importante:</p>
      <ol class="search-ol">
        <li><span>Conocer la ferretería donde deseas realizar la solicitud. <a class="link-pdf" href="https://construya.com/images/ubicacion_ferreterias.pdf" target="_blank">Identifica aquí las ferreterías que tienes cerca.</a></span></li>
        <li><span>Cédula original.</span></li>
        <li><span>Tener celular (Smartphone)</span></li>
        <li><span>Activar los permisos de ubicación de tu celular</span></li>
      </ol>
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
        ciudad: ''
      },
      resultsActive: false,
      mobile: false,
    }
  },
  emits: ['idSelected'],
  watch: {
    searchQuery: function(newValue) {
      if (newValue.length ==0) {
        this.resultsActive = false;
      }
      // console.log("watch:"+newValue);
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
      this.selected.ciudad = '';
      this.searchActive = this.data;
    },
    select(id, name, ciudad) {
      this.searchQuery = '';
      this.resultsActive = false;
      this.selected.id = id;
      this.selected.name = name;
      this.selected.ciudad = ciudad;
    },
    checkMobile() {
      if(window.innerWidth < 768){
        this.mobile = true;
      }
    },
    removeAccents(str) {
      return str.normalize("NFD").replace(/[\u0300-\u036f]/g, "");
    },
    search() {
      //takes query String to search in data Array that contains object with name and id
      //returns array of objects that match the query
      if(this.searchQuery.length>0){
        this.resultsActive = true;
      }
      this.searchActive = this.data;
      const searchNormalize = this.removeAccents(this.searchQuery.toLowerCase());
      //takes this.searchQuery and searches in this.data Object to return an array of objects that match the query
      this.searchActive = this.searchActive.filter(function (item) {
        let itemName = item.name.toLowerCase();
        itemName = this.removeAccents(itemName);
        let itemCiudad = item.ciudad.toLowerCase();
        itemCiudad = this.removeAccents(itemCiudad);
        // console.log(item);
        return (itemName.includes(searchNormalize) || itemCiudad.includes(searchNormalize));
      }.bind(this));


    },
    sendToPage() {
      if(this.selected.id.length){
        this.$emit('idSelected', this.selected.id);
      }
    },
  },
  mounted() {
    this.importData();
    this.checkMobile();
  }
}

</script>
<style lang="scss">
.head-text{
  text-align: center;
}
.selected{
  position: absolute;
  top: 5px;
  display: block;
  background: #fbbd0f;
  z-index: 999;
  padding: 2px 24px;
  font-size: 16px;
  line-height: 16px;
  width: 68%;
  left: 6px;
  border-radius: 5px;
  border: 1px solid grey;
  span{
    font-weight: 700;
  }
}
.close{
  width: 32px;
  height: 100%;
  position: absolute;
  text-align: center;
  right: 1px;
  top: 0;
  display: grid;
  align-content: center;
  background-color: #fb980f;
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
  color: #2c3e50;
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
  column-gap:5px;

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
  height: calc(3rem + 2px);
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  color: #495057;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: 0.25rem 0 0 0.25rem;
  transition: border-color .15s ease-in-out, box-shadow .15s ease-in-out;
}

.card {
  //background-color: rgb(249, 249, 249);
  /*box-shadow: 0 8px 17px 0 rgb(55 55 55 / 20%), 0 6px 20px 0 rgb(125 125 125 / 19%);*/
  position: relative;
  margin: 10px 0 20px 0;
  border-radius: 8px;
  /*background: #c4d600;*/
  /*background-color: white;*/
  /*background-color: white;*/
  padding: 0;
  &--header {
     padding: 20px 0px;
     display: grid;
     text-align: left;
     justify-items: center;
   }

  &--content {
    border-radius: 0 0 2px 2px;
    padding: 0 0 20px 0;
  }
}
.search-ol {
  color: #00356d;
  padding-left: 15px;
}
.search-ol li {
  font-weight: bold;
}
.search-ol span {
  color: #495057;
  font-weight: normal;
  font-size: 16px;
  font-style: normal;
}
.link-pdf {
  color: #00356d;
  font-weight: bold;
  font-style: italic;
}

</style>