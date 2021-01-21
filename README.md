# Описание
Компонент разработан для версии Vue 2

# Установка
Чтобы установить компонент в консоле необходимо ввести команду:
```bash
$ npm install @hwt/vue-datepicker
```

# Использование
```javascript
<template>
    <div>
        <date-picker />
    </div>
</template>
<script>
    import DatePicker from '@hwt/vue-datepicker'
    import '@hwt/vue-datepicker/src/assets/scss/index.scss'

     export default{
        components: {
            DatePicker
        },
        data(){
            return {}
        }
     }
</script>
```

# Входные параметры:
| Наименование | Тип данных | Описание |
|:----------------:|:---------:|:----------------:|
|date| Date | берется месяц которы будет отображаться|
| week-names | Array | локализация полных названий дней недели где 0 - Воскресенье, 1 - Понедельник |
| month-names | Array | локализация полных названий месяцев |
| week-names-short | Array | локализация сокращенных названий дней недели где 0 - Воскресенье, 1 - Понедельник |
| multiple | Boolean | устанавливается возможность выбора диапазона даты |
| marked-date | Array | массив дат класса Date которые по умолчанию будут отмечены |
| count | Number | Количество календарей |
