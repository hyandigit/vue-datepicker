<template>
    <div :class="classList">
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
            }
        },
        data()
        {
            return {

            };
        },
        computed:{
            classList()
            {
                return {
                  'day': true,
                  'fill': (this.date.getMonth() != this.currentDate.getMonth())
                };
            }
        }
    }
</script>

<style scoped>

</style>