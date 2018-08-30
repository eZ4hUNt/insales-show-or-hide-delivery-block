# Скрываем или показываем блок доставки в чекауте InSales
В данной реализации, если город не выбран или несуществующий, то скрываем блок доставки

Добавляем скрипт в шаблон чекаута:
```
	<script>
		// Скрываем или показываем блок доставки
                    var city_status ;
                    $('#shipping_address_full_locality_name').on('input keyup', function(e) {
                        city_status = $('.tt-dataset-0').find('.empty-message').html();
                        console.log(city_status);
                    });

                    function delivery_block(city_status){
                        if($('#shipping_address_full_locality_name').val() == ''){
                            $('#co-delivery').find('.co-delivery_method').parent().hide();
                        }else{
                            if(city_status == 'Город не найден'){
                                $('#co-delivery').find('.co-delivery_method').parent().hide();
                            }else{
                                $('#co-delivery').find('.co-delivery_method').parent().show();
                            }
                        }
                    }

                    delivery_block(city_status);


                    $('#shipping_address_full_locality_name').on('change', function(e) {
                        delivery_block(city_status);
                            setTimeout(function() {
                                $('#delivery_variants input').trigger("change");
                            }, 1000);
                    });

                    $(document).mouseup(function (e){ // событие клика по веб-документу
                        var div = $("#shipping_address_full_locality_name"); // тут указываем ID элемента
                        if (!div.is(e.target)){
                            delivery_block(city_status);
                            setTimeout(function() {
                                $('#delivery_variants input').trigger("change");
                            }, 1000);

                        }
                    });
	</script>
```

## Сам скрипт и пример на GitHub
https://github.com/eZ4hUNt/insales-show-or-hide-delivery-block

Пример: https://www.asobu.ru/new_order
