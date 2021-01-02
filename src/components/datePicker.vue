<template>
    <div class="datepicker">
        <div class="month-name">
            <span v-show="!(show & 0)" class="prev" v-on:click="onChangeMonth(-1)">&#60;&#60;</span>
            <span class="name">{{monthNames[currentDate.getMonth()]}}</span>
            <span v-show="!(show & 1)" class="next" v-on:click="onChangeMonth(1)">&#62;&#62;</span></div>
        <div class="weeks">
            <div class="week-day-name" v-for="week in weeks" :key="week">{{weekNamesShort[week]}}</div>
        </div>
        <div class="days">
            <day v-for="(day, index) in listDays" :key="index" 
                :date="day" 
                :selected-date="selectedDate"
                :current-date="currentDate"
                v-on:click="onClickDay(day)"
            >
            </day>
        </div>
    </div>
</template>

<script>
    import Day from "./day";
    export default {
        name: "month",
        components: {Day},
        props: {
            //биты отображения
            //какие элементы календаря скрывать
            // 0 - Стрелка переключения месяца влево
            // 1- Стрелка переключения месяца вправо
            show:{
                type: Number,
                default: () => 0
            },
            date:{ //дата месяца который будет отображатся
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
            monthNames:{
                type: Array,
                default: () => {
                    return [
                        'Январь',
                        'Февраль',
                        'Март',
                        'Апрель',
                        'Май',
                        'Июнь',
                        'Июль',
                        'Август',
                        'Сентябрь',
                        'Октябрь',
                        'Ноябрь',
                        'Декабрь'
                    ];
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
            },
            multiple:{
                type: Boolean,
                default: () => false
            },
            markedDate:{
                type: Array,
                default: () => []
            }
        },
        data()
        {
            return {
                weeks:[1,2,3,4,5,6,0],
                selectedDate: [],
                addMonthNumber: 0, //смещение месяца
            };
        },
        watch: {

        },
        methods:{
            onClickDay(date) //события клика по дню
            {
                console.log('onClickDay', this.multiple);
                if(!this.multiple){
                    this.$set(this.selectedDate, 0, date);
                }
            },
            onChangeMonth(add) //событие при смене месяца
            {
                this.addMonthNumber += add;
            }
        },
        computed:{
            startDate() //с какого дня отрисовываем календарь
            {
                let date = new Date(this.currentDate.getTime());
                date.setDate(1);
                if(date.getDay() == 0){
                    date.setDate(date.getDate() - 7);
                }
                date.setDate((date.getDate() - date.getDay()) + 1); // +1 смещаем отрисувку дней на один чтобы старт недели был понедельник
                return date;
            },
            numberDays() //подсчитываем количество дней для отрисовки
            {
                let count = 0;
                let date = new Date(this.currentDate.getTime());
                date.setMonth(date.getMonth() + 1);
                date.setDate(0);
                date.setDate(date.getDate() + (7 - (date.getDay())));
                count = (date.getTime() - this.startDate.getTime()) / 86400000;
                return count;
            },
            listDays() //массив дней календаря
            {
                let data = [];
                for(let i = 0; i <= this.numberDays; i++){
                    data.push(new Date(this.startDate.getFullYear(), this.startDate.getMonth(), this.startDate.getDate() + i));
                }
        
                return data;
            },
            currentDate() //дата старта отображения календаря
            {
                return new Date(this.date.getFullYear(), this.date.getMonth() + this.addMonthNumber, this.date.getDate());
            }

        }
    }
</script>

<style scoped>

</style>