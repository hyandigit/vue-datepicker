<script>
    import Day from "./day";
    export default {
        name: "month",
        components: {Day},
        render(h) 
        {
            let self = this;
            return h('div', {class: 'datepicker'},
            [
                h('span', { class: 'month-name'}, [
                    h('span', { class: 'prev', on:{click: () => { self.onChangeMonth(-1) }}, style: 'display:' + (!(self.show & 0) ? 'initial' : 'none') }, '<<'),
                    h('span', { class: 'name', on:{click: () => { self.onChangeMonth(-1) }} }, self.monthNames[self.currentDate.getMonth()]),
                    h('span', { class: 'prev', on:{click: () => { self.onChangeMonth(1) }}, style: 'display:' + (!(self.show & 1) ? 'initial' : 'none')}, '>>'),
                ]
                ),
                h('div', { class: 'weeks'}, self.weeks.map((week) => {
                        return h('div', { class: 'week-day-name' }, self.weekNamesShort[week]);
                    })
                 ), 
                h('div', { class: 'days'}, self.listDays.map((day) => {
                        return h('day', { 
                            class: 'week-day-name', 
                            props:{ 
                                date: day, 
                                'selected-date': self.selectedDate, 
                                'current-date': self.currentDate, 
                                'marked-date': self.markedDate 
                            }, 
                            on:{ click: () => { self.onClickDay(day) }},
                            scopedSlots: self.$scopedSlots, 
                            });
                    })
                 ),
            ]
            );
        },
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
            multiple:{ //знак выбора диапазона дат
                type: Boolean,
                default: () => false
            },
            markedDate:{ //даты которые необходимо отметить как выбранное
                type: Array,
                default: () => []
            },
            selectedDate:{ // выбранная дата
                type: Array,
                default: () => []
            }
        },
        data()
        {
            return {
                weeks:[1,2,3,4,5,6,0],
                addMonthNumber: 0, //смещение месяца
            };
        },
        watch: {

        },
        methods:{
            onClickDay(date) //события клика по дню
            {
                this.$emit('click', date);
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