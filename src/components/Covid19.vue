<template>
  <div class="container">
    <div>
     <div>
  <b-card
    overlay
    img-src="https://www.escardio.org/static-file/Escardio/Medias/education/covid-19/Covid-19-Webpage-banner-1170x240-opt2.jpg?mts=1594053162000.jpg"
    img-alt="Card Image"
    text-variant="black"
    title="Covid-19 Günlük Bilginlendirme Kitapçığı"
    sub-title="covid19.eraybulut34.com"
    img-height="100"
  >
    <b-card-text>
      Kendiniz ve sevdikleriniz için, covid19 önlemlerine karşı duyarlı olun.
    </b-card-text>
  </b-card>
</div>
<div class="col-md-12">
        <b-tabs content-class="col-md-12">
        <b-tab title="Dünya Genelinde Aşı" active>
          <!-- <div> -->
            <div>
            <b-table striped hover :items="vaccinated" :fields='[{key:"country",sortable:false},{key:"timeline",sortable:true}]'>
              <template #cell(timeline)="data">
                {{Object.entries(data.item.timeline)[0][1]}}
              </template>
            </b-table>
            </div>
            <!-- <div v-for="item in vaccinated" :key="item.country"><b>{{item.country}}|{{Object.entries(item.timeline)[0][1]}}</b></div></div> -->
        </b-tab>
        <b-tab title="Dünya Geneli Son Durum">
            <div class="col-md-12">  
<table class="table table-bordered">
  <tr>
     <td>Toplam Vaka</td>
     <button class="btn btn-danger">{{AllData.cases}}</button>
  </tr>
  <tr>
    <td>Günlük Vaka</td>
    <button class="btn btn-danger">{{AllData.todayCases}}</button>
  </tr>
   <tr>
    <td>Ölüm Sayısı</td>
    <button class="btn btn-dark">{{AllData.deaths}}</button>
  </tr>
   <tr>
    <td>Günlük Ölüm</td>
    <button class="btn btn-dark">{{AllData.todayDeaths}}</button>
  </tr>
   <tr>
    <td>İyileşen</td>
    <button class="btn btn-success">{{AllData.recovered}}</button>
  </tr>
   <tr>
    <td>Günlük İyileşen</td>
    <button class="btn btn-success">{{AllData.todayRecovered}}</button>
  </tr>
   <tr>
    <td>Aktif Vaka</td>
    <button class="btn btn-warning">{{AllData.active}}</button>
  </tr>
   <tr>
    <td>Kritik Durumda Olanlar</td>
    <button class="btn btn-secondary">{{AllData.critical}}</button>
  </tr>
   <tr>
    <td>Her 1 Milyonda Vaka</td>
    <button class="outline-primary">{{AllData.casesPerOneMillion}}</button>
  </tr>
   <tr>
    <td>Her 1 Milyonda Ölüm</td>
    <button class="btn btn-dark">{{AllData.deathsPerOneMillion}}</button>
  </tr>
   <tr>
    <td>Yapılan Test</td>
    <button class="btn btn-primary">{{AllData.tests}}</button>
  </tr>
   <tr>
    <td>Her 1 Milyonda Test</td>
    <button class="btn btn-light">{{AllData.testsPerOneMillion}}</button>
  </tr>
</table>
</div>
        </b-tab>
        </b-tabs>
    </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      vaccinated: "",
      AllData: 0,
    };
  },
  beforeMount() {
    this.getdata();
    this.getAllData();
  },
  methods: {
    getdata() {
      axios
        .get(
          "https://disease.sh/v3/covid-19/vaccine/coverage/countries?lastdays=1"
        )
        .then((response) => {
          this.vaccinated = response.data;
        });
    },
    getAllData(){
      axios.get("https://disease.sh/v3/covid-19/all").then((response) => {
        this.AllData = response.data;
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
