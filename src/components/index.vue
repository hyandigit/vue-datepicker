<script>
import Month from './datePicker';
export default {
    'name': 'datePicker',
    render(h) 
    {
        let childs = [];
        let self = this;
        for(let i = 0; i < self.countDatePicker; i++){
            childs.push(h('month', {
                props: {
                    date: self.monthDate(i),
                    'selected-date': self.selectedDate
                },
                on:{
                    click: self.onClickDay
                },
                scopedSlots: self.$scopedSlots,
            }));
        }
        return h('div', {class: 'calendars'}, childs);
    },
    components:{
        Month
    },
    props:{
        date: { //дата старта отрисовки
            type: Date,
            default: () => (new Date)
        },
        mode: { //режим календаря
            type: Number,
            default: () => 0
        },
        show:{
            type: Number,
            default: () => 0
        },
        weekNames:{ //переводы названия дней недели
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
        monthNames:{ //переводы названия месяцев
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
        weekNamesShort:{ //переводы сокращенных названий дней недели
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
        markedDate:{ //дни которые необходимо отметить как выбранные
            type: Array,
            default: () => []
        },
        count:{
            type: Number,
            default: () => 1
        },
        multiple:{
            type: Boolean,
            default: () => false
        },
    },
    data()
    {
        return {
            weeks:[1,2,3,4,5,6,0],
            selectedDate: [],
            multipleStart: false
        };
    },
    methods:{
        onClickDay(date) //события клика по дню
        {
            if(!this.multiple){
                this.$set(this.selectedDate, 0, date);
            }else{ //диапазон выбора               
                if(!this.multipleStart){
                    this.selectedDate = [];
                    this.multipleStart = true;
                }
                if(this.multipleStart && (this.selectedDate.length == 0)){console.log(1);
                    this.$set(this.selectedDate, 0, date);
                }else if(this.multipleStart && (this.selectedDate.length > 0)){console.log(3);
                    this.$set(this.selectedDate, 1, date);
                    this.multipleStart = false;
                }
            }
            this.$emit('input', this.selectedDate);
        },
        monthDate(index) //начальная дата календаря
        {
            let date = new Date(this.date.getTime());
            if(this.count){
                date.setMonth(date.getMonth() + index);
                return date;
            }
            return this.date;
        }
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
    },
    cteated()
    {
    }
}
</script>
<style scoped>

</style>