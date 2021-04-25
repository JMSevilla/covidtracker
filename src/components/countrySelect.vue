<template>
    <div>
        <el-select v-model="selected" @change="onChange()" style="width: 100%;" filterable placeholder="Select countries">
        <el-option
        v-for="item in countries"
        :key="item.ID"
        :label="item.Country"
        :value="item.ID">
        </el-option>
    </el-select>
    </div>
</template>

<script>
export default {
    props: ['countries'],
    data() {
        return { 
            selected: ''
        }
    },
    methods : {
        onChange() {
            const country = this.countries.find((item) => item.ID === this.selected)
            
             this.$emit('get-country', country)
        }
    }
}
</script>