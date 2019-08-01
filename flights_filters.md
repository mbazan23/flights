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
Veremos que los resultados filtrados suman la cantidad del total (54 = 0 + 7 + 43)

Busquemos la cantidad de vuelos con 0 stop. Resultado 0 segmentos encontrados

```ruby
>> p filter_segmets_for_amount_of_stop(data, segments, 0).size
0
```
Busquemos la cantidad de vuelos con 1 stop . Resultado 7 segmentos encontrados
```ruby
>> p filter_segmets_for_amount_of_stop(data, segments, 1).size
7
```
Por ultimo  la cantidad de vuelos con 2 stops. Resultado 43 segmentos encontrados
```ruby
>> p filter_segmets_for_amount_of_stop(data, segments, 2).size
47
```

### Filtros por Aerolinea

En este Json en particular, cada segmento tiene una unica Aerolinea asignada,
por eso 28 + 7 + 19 = 54 que es el total. Pero si los segmentos tuviesen varias
aerolineas, todas las aerolineas que esten contenidas y esten en la busqueda haran 
que el segmento aparezca.

Cantidad de Vuelos de la aerolinea "United" :
```ruby
>> p filter_segmets_by_airlines(data, segments, "United").size
28
```
Cantidad de Vuelos de la aerolinea "American Airlines" :
```ruby
>> p filter_segmets_by_airlines(data, segments, "American Airlines").size
7
```
Cantidad de Vuelos de la aerolinea "Delta" :
```ruby
>> p filter_segmets_by_airlines(data, segments, "Delta").size
19
```





### Avanzar al segundo segmentos
Cuando se elige el primer segmento, ahora lo se debera elegir el siguiente
Como es de esperar la lista de segmentos disponibles se acota. Podemos comprobar
esto facimente

Primero cargamos la lista de segundos segmentos disponibles, eligiendo antes el codigo del primer segmento
```ruby
>> second_segments = get_segments(data, ["ZFS-WEB-AA1211-DFW-MSY-1555440240-SUAIZNM1-S"])
>> p second_segments.size

7
```

### Avanzar al tercer segmento
Como hicimos con el segundo segmento, ahora elegimos los terceros segmentos disponibles , recordando
poner como condicion inicial los dos segmentos previamente seleccionados.
```ruby
>> third_segments = get_segments(data, ["ZFS-WEB-AA1211-DFW-MSY-1555440240-SUAIZNM1-S"])
>> p third_segments.size

```

### Sobre filtros y orden 
Como vimos, los filtros y metodos de ordenamientos se aplican por segmentos, por lo que 
los mismos que se aplicaron al principio con el primer segmentos , son aplicables a cualquier 
segmento sucesivo.
