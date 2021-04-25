<template>
    <div>
        <navbar />
        <div class="container" style="margin-top: 2rem;">
            <dataTitle :text="title" :dataDate="dataDate" />
            <div class="row mt-5">
               <div class="col-sm">
                    <dataBoxes :stats="stats" />
               </div>
               
            </div>
            <div class="mt-3">
                <countrySelect @get-country="getCountryData" :countries="countries" />
                <div class="mt-2">
                      <el-button type="success" plain @click="onclear()">Clear</el-button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import dataTitle from "@/components/dataTitle"
import dataBoxes from "@/components/dataBoxes"
import countrySelect from "@/components/countrySelect"
import navbar from "@/components/navbar"
export default {
    components : {
        navbar,
        dataTitle, dataBoxes, countrySelect
    },
    data() {
        return { 
            loading: true,
            title: 'Global',
            dataDate : '',
            stats: {},
            countries: []
        }
    },
    methods: {
        async fetchCovidData() {
            const res = await fetch('https://api.covid19api.com/summary')
            const data = await res.json()
            return data
        },
        getCountryData(country) { 
            this.stats = country
            this.title = country.Country
        },
        async onclear() 
        {
            const loading = this.$loading({
          lock: true,
          text: 'Fetching Original API',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)'
        });
             const data = await this.fetchCovidData()
        this.dataDate = data.Date
        this.stats = data.Global
        this.countries = data.Countries
        this.title = 'Global'
        loading.close()
        }
    },
    async created() {
         const loading = this.$loading({
          lock: true,
          text: 'Fetching API',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)'
        });
        const data = await this.fetchCovidData()
        this.dataDate = data.Date
        this.stats = data.Global
        this.countries = data.Countries
        loading.close()
    }
}
</script>