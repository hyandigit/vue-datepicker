<template>
    <div class="datepicker">
        <div class="month-name">Январь</div>
        <div class="weeks">
            <div class="week-day-name" v-for="week in weeks" :key="week">{{weekNamesShort[week]}}</div>
        </div>
        <div class="days">
            <day v-for="(day, index) in listDays" :key="index" :date="day" :current-date="currentDate"></day>
        </div>
    </div>
</template>

<script>
    import Day from "./day";
    export default {
        name: "datePicker",
        components: {Day},
        props: {
            currentDate:{
                type: Date,
                default: () => (new Date)
            },
            weekNames:{
                type: Array,
                default: () => {
                    return [
                        'Восресенье',
                        'Понедельник',
                        'Вторник',
                        'Среда',
                        'Четверг',
                        'Пятница',
                        'Суббота',
                    ]
                }
            },
            weekNamesShort:{
                type: Array,

                default: () => {
                    return [
                        'Вс',
                        'Пн',
                        'Вт',
                        'Ср',
                        'Чт',
                        'Пт',
                        'Сб',
                    ]
                }
            }
        },
        data()
        {
            return {
                weeks:[0,1,2,3,4,5,6]
            };
        },
        watch: {

        },
        methods:{

        },
        computed:{
            startDate() //с какого дня отрисовываем календарь
            {
                let date = new Date(this.currentDate.getTime());
                date.setDate(1);
                date.setDate(date.getDate() - date.getDay());
                return date;
            },
            numberDays() //подсчитываем количество дней для отрисовки
            {
                let count = 0;
                let date = new Date(this.currentDate.getTime());
                date.setDate(1);
                count += date.getDay();
                date.setMonth(date.getMonth() + 1);
                date.setDate(0);
                count += date.getDate() + (7 - (date.getDay() + 1));
                return count;
            },
            listDays()
            {
                let data = [];
                for(let i = 0; i < this.numberDays; i++){
                    data.push(new Date(this.startDate.getTime() + (i * 86400000)));
                }
                return data;
            }
        }
    }
</script>

<style scoped>

</style>