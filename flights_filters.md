<!--
Load the necessary libraries
>> require_relative 'filter_and_sort_functions_for_segments.rb'
<...>
-->

Cargamos un set de initerarios desde el archivo 'flights.json', el cual se encuentra normalizado, con 
este set realizaremos todas las pruebas que vendran.

```ruby
>> data = JSON.parse(File.read('flights.json'))
<...>
```

## Elejir el primer segmento

En primera instancia podremos ver todos los segmentos disponibles que podemos elegir como primer segmento
Notar que get_segments pasa una lista vacia indica que aun no se eligio ningun segmento
```ruby
>> segments = get_segments(data, [])
>> segments.each do |segment|
..  pp segment
.. end
{:airlines=>["American Airlines"],
 :departure_time=><...>,
 :duration=><...>,
 :from=><...>,
 :to=><...>,
 :zid=><...>}
<...>

```
Como se ve arriva, moostramos el primer resultado ya que este set list es tiene 54 primeross segmentos disonibles para elegir.

Luego comprobamos la cantidad de resultados obtenidos
```ruby
>> segments.size

```
## Aplicar Filtros sobre los segmentos
Ahora empezaremos a poner ciertas condiciones, y veremos como la cantidad de segmentos se reducen en base
a los filtros elegidos

#### Filtro segun cantidad de paradas (Stops)

Bien, ahora elegimos el siguiente segmento( veremos que la cantidad de segmentos disponibles disminuye)
Para ir al siguiente segmento elegimos el sesgmento que queremos, en este caso elegimos el del resultado anterior


Busquemos la cantidad de vuelos con 0 stop 

```ruby
>> filter_segmets_for_amount_of_stop(data, second_segments, 0).size

```
Busquemos la cantidad de vuelos con 1 stop 
```ruby
>> filter_segmets_for_amount_of_stop(data, second_segments, 1).size

```
Por ultimo  la cantidad de vuelos con 2 stops
```ruby
>> filter_segmets_for_amount_of_stop(data, second_segments, 2).size

```











```ruby
>> segments = get_segments(data, ["ZFS-WEB-AA1211-DFW-MSY-1555440240-SUAIZNM1-S"])
>> segmets.each do |segment|
..  pp segment
.. end
{:airlines=>["American Airlines"],
 :departure_time=>"2019-04-30T19:11:00",
 :duration=>"PT1H44M",
 :from=>"New Orleans",
 :to=>"Dallas",
 :zid=>"ZFS-WEB-AA2257-MSY-DFW-1556669460-NVAIUSM1-N"}
<...>

```

Podemos comprobar que disminuyeron los segmentos disponibles para elegir
```ruby
>> second_segments.size

```

##Probemos Los Filtros

Sobre el segundo segmento probamos los filtros

Filtrar por Cantidad de Stops
Busquemos la cantidad de vuelos con 0 stop 

```ruby
>> filter_segmets_for_amount_of_stop(data, second_segments, 0).size

```
Busquemos la cantidad de vuelos con 1 stop 
```ruby
>> filter_segmets_for_amount_of_stop(data, second_segments, 1).size

```
Por ultimo  la cantidad de vuelos con 2 stops
```ruby
>> filter_segmets_for_amount_of_stop(data, second_segments, 2).size

```



