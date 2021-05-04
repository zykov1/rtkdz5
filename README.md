# Домашнее задание 5: контроль качества данных с фреймворком Great Expectations #

# izykov.ods_payment #

## pay_doc_type + pay_doc_num ##

- Эти поля должны являться уникальными вместе - быть "бизнесовым PK"
batch.expect_compound_columns_to_be_unique(column_list=['pay_doc_type', 'pay_doc_num'])

## user_id ## 

- Не должно быть данных с NULL
batch.expect_column_values_to_not_be_null(column='user_id')

- Проверка на тип данных (можно везде опустить, т.к. проверяет БД, но на всяк.случай оставляю)
batch.expect_column_value_s_to_e_of_type(column='user_id', type_='INTEGER')

## pay_doc_type ## 

- Не должно быть данных с NULL
batch.expect_column_values_to_not_be_null(column='pay_doc_type')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='pay__doc_tpe', type_='TEXT')

- Соответствие значения допустимому списку  
batch.expect_column_distinct_values_to_be_in_set(column='pay_doc_type', value_set=['MASTER', 'MIR', 'VISA'])

- В наборе данных должны присутствовать все значения из списка  
batch.expect_column_distinct_values_to_equal_set(column='pay_doc_type', value_set=['MASTER', 'MIR', 'VISA'])

## pay_doc_num ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='pay_doc_num')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='pay_doc_num', type_='INTEGER')

## account ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='account')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='acco_unt',type_='TEXT')

- Все значения столбца должны соответствовать регулярному выражению  
batch.expect_column_values_to_match_regex(column='account', regex='^FL-\d+$')

## phone ## 

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='phone', type_='NUMERIC')

- Более быстрая (чем regex) и изящная проверка, что все телефоны - российские (при необходимости можно добавить других проверок)
batch.expect_column_values_to_be_between(column='phone', max_value=79999999999, min_value=70000000000)

## billing_period ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='billing_period')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='billing_period', type_='DATE')

- Проверка на то, что данные попадают в заданный диапазон  
batch.expect_column_values_to_be_between(column='billing_period', max_value='2022-01-01', min_value='2013-01-01')

## pay_date ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='pay_date')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='pay_date', type_='TIMESTAMP')

- Проверка на то, что данные попадают в заданный диапазон  
batch.expect_column_values_to_be_between(column='pay_date', max_value='2022-01-01', min_value='2013-01-01')

## sum ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='sum')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='sum', type_='INTEGER')

- Допустим, что платеж должен быть > 0 и меньше 1 миллиарда
batch.expect_column_values_to_be_between(column='sum', max_value=999999999, min_value=0)

# izykov.ods_traffic #

- Не должно быть данных с NULL 
batch.expect_column_values_to_not_be_null(column='user_id')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='user_id', type_='INTEGER')  

## time_stamp ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='time_stamp')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='time_stamp', type_='TIMESTAMP')

- Проверка на то, что данные попадают в заданный диапазон  
batch.expect_column_values_to_be_between(column='timestamp_', max_value='2022-01-01', min_value='2013-01-01')

## device_id ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='device_id')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='device_id', type_='TEXT')

- Все значения столбца должны соответствовать регулярному выражению  
batch.expect_column_values_to_match_regex(column='device_id', regex='^d\d{3}$')

## device_ip_addr ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='device_ip_addr')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='device_ip_addr', type_='TEXT')

## bytes_received ## 

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='bytes_received', type_='INTEGER')

## bytes_sent ## 

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='bytes_sent', type_='INTEGER')

# izykov.ods_billing #

## user_id ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='user_id')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='user_id', type_='INTEGER')

## billing_period ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='billing_period')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='bill_ing_priod', type_='DATE')

- Проверка на то, что данные попадают в заданный диапазон  
batch.expect_column_values_to_be_between(column='billing_period', max_value='2022-01-01', min_value='2013-01-01')

## service ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='service')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='service', type_='TEXT')

- Соответствие значения допустимому списку  
batch.expect_column_distinct_values_to_be_in_set(column='service', value_set=['Connect', 'Disconnect', 'Setup Environment'])

## tariff ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='tariff')

- Проверка на тип данных  
batch.expect_column_values_to_not_be_null(column='tariff')

- Соответствие значения допустимому списку  
batch.expect_column_distinct_values_to_be_in_set(column='tariff', value_set=['Maxi', 'Mini', 'Gigabyte', 'Megabyte'])

## sum ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='sum')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='sum', type_='INTEGER')

- Допустим, что платеж должен быть > 0 и меньше 1 миллиарда
batch.expect_column_values_to_be_between(column='sum', max_value=999999999, min_value=0)

## created_at ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='created_at')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='created_at', type_='DATE')

- Проверка на то, что данные попадают в заданный диапазон  
batch.expect_column_values_to_be_between(column='created_at', max_value='2022-01-01', min_value='2013-01-01')


# izykov.ods_issue #

## user_id ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='user_id')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='user_id', type_='INTEGER')

## start_time ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='start_time')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='star_t_tim', type_='TIMESTAMP')

- Проверка на то, что данные попадают в заданный диапазон  
batch.expect_column_values_to_be_between(column='start_time', max_value='2022-01-01', min_value='2013-01-01')

## end_time ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='end_time')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='end_time', type_='TIMESTAMP')

- Проверка на то, что данные попадают в заданный диапазон  
batch.expect_column_values_to_be_between(column='end_time', max_value='2022-01-01', min_value='2013-01-01')

## title ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='title')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='title', type_='TEXT')


## description ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='description')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='description', type_='TEXT')

## service ## 

- Не должно быть данных с NULL   
batch.expect_column_values_to_not_be_null(column='service')

- Проверка на тип данных  
batch.expect_column_values_to_be_of_type(column='service', type_='TEXT')

- Соответствие значения допустимому списку  
batch.expect_column_distinct_values_to_be_in_set(column='service', value_set=['Connect', 'Disconnect', 'Setup Environment'])
