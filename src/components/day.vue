<template>
    <div v-on:click="onClick()" :class="classList">
        <span>{{date.getDate()}}</span>
    </div>
</template>

<script>
    export default {
        name: "day",
        props:{
            date:{
                type: Date
            },
            currentDate:{
                type: Date
            },
            selectedDate:{
                type: Array,
                default: () => []
            }
        },
        data()
        {
            return {

            };
        },
        methods:{
            checkInRange()
            {
                if(this.selectedDate.length){
                    if(this.selectedDate.length == 2){
                        return (this.selectedDate[0].getTime() <= this.date.getTime()) 
                                && (this.selectedDate[1].getTime() >= this.date.getTime())
                    }else{
                        return this.selectedDate[0].getTime() == this.date.getTime();
                    }
                }
            },
            onClick()
            {
                this.$emit('click', this.date);
            }
        },
        computed:{
            classList()
            {
                return {
                    'day': true,
                    'fill': (this.date.getMonth() != this.currentDate.getMonth()),
                    'selected' : this.checkInRange()
                };
            }
        }
    }
</script>

<style scoped>

</style>