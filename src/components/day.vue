<template>
    <div v-on:click="onClick()" :class="classList">
        <slot name="day" v-bind:day="date">
            <span>{{date.getDate()}}</span>
        </slot>
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
            },
            markedDate:{ //даты которые необходимо отметить как выбранное
                type: Array,
                default: () => []
            },
        },
        data()
        {
            return {

            };
        },
        methods:{
            checkInRange()
            {
                if(this.date.getMonth() != this.currentDate.getMonth()){
                    return false;
                }
                if(this.selectedDate.length){
                    if(this.selectedDate.length == 2){
                        return (this.selectedDate[0].getTime() <= this.date.getTime()) 
                                && (this.selectedDate[1].getTime() >= this.date.getTime())
                    }else{
                        return this.selectedDate[0].getTime() == this.date.getTime();
                    }
                }else if(this.markedDate.length){
                    for(let i = 0; i < this.markedDate.length; i++){
                        if(Array.isArray(this.markedDate[i])){
                        return (this.markedDate[i][0].getTime() <= this.date.getTime()) 
                                && (this.markedDate[i][1].getTime() >= this.date.getTime())
                        }else{
                            return this.markedDate[i].getTime() == this.date.getTime();
                        }
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