<template>
    <div>
        <div class="card bg-dark text-light">
            <div class="card-body text-center">
                <h2>Cases</h2>
                <div class="text-2xl mb-4">
                    <span style="font-weight: bold;">New:</span>
                {{numberism(stats.NewConfirmed)}}
                </div>
                <div class="text-2xl mb-4">
                    <span style="font-weight: bold;">Total:</span>
                {{numberism(stats.TotalConfirmed)}}
                </div>
            </div>
        </div>

        <div class="card bg-dark text-light mt-3">
            <div class="card-body text-center">
                <h2>Deaths</h2>
                <div class="text-2xl mb-4">
                    <span style="font-weight: bold;">New:</span>
                {{numberism(stats.NewDeaths)}}
                </div>
                <div class="text-2xl mb-4">
                    <span style="font-weight: bold;">Total:</span>
                {{numberism(stats.TotalDeaths)}}
                </div>
            </div>
        </div>
        
    </div>
</template>

<script>
export default {
    props: ['stats'],
    methods : {
        numberism(x) { 
            return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
        }
    }
}
</script>