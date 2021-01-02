<template>
    <div>
        <month v-for="item in countDatePicker" :key="item"
            :date="date"></month>
    </div>
</template>
<script>
import Month from './datePicker';
export default {
    'name': 'datePicker',
    components:{
        Month
    },
    props:{
        date: {
            type: Date,
            default: () => (new Date)
        },
        mode: {
            type: Number,
            default: () => 0
        },
        show:{
                type: Number,
                default: () => 0
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
        markedDate:{
            type: Array,
            default: () => []
        },
        count:{
            type: Number,
            default: () => 0
        }
    },
    methods:{

    },
    computed:{
        countDatePicker()
        {
            let count = this.count;
            if(!count){
                switch(this.mode){
                    case 2:
                    count = 2;
                    break;
                    default:
                    count = 1;
                    break;
                }
            }
            return count;
        }
    }
}
</script>