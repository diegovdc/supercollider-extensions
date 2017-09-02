# supercollider extensions

## Classes/Object
### `pipe`  

Aplica una función a `this` y regresa el resultado de esa función.  Resulta útil para aplicar funciones encadenadas.
 
 Ejemplo Básico:
 ```
 ~timesTwo = {|n| 2*n};
 ~toArray = {|n| [n]};
 
 5.pipe(~timesTwo).pipe(~toArray)// [10]

//equivalente a:
~toArray.(~timesTwo.(5))
 ```

 Ejemplo de uso real:
```
//Permite transformar esto:
(
var melodia = ~concat.(//concatena la ~melodiaEnArrays -- e.g [["B4"], ["C5", "Bb6"]] -> ["B4", "C5", "Bb6"]
	~melodiaEnArrays 
		.collect(_.namemidi)
		.collect(_.midicps));
~taskMaker.(melodía,\miSynthdef).play //inyecta la melodia junto con un SynthDef a una función que genera un Task 
)

//en esto:
(
~melodiaEnArrays
	.collect(_.namemidi) 
	.collect(_.midicps) 
	.pipe(~concat.(_)) // hasta aquí lo que arriba es la variable "melodía"
	.pipe(~taskMaker.(_, \miSynthdef)) //inyecta la melodia junto con un SynthDef a una función que genera un Task 
	.play 
)
```