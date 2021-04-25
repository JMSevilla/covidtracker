<template>
    <div class="text-center">
        <h3 >{{text}}</h3>
        <p >{{timestamp}}</p>
    </div>
</template>

<script>
import moment from 'moment'
export default {
    props: ['text', 'dataDate'],
   computed: {
       timestamp : function() {
           return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
       }
   }
}
</script>