# supercollider extensions

## Classes/Object
### `pipe`  
Aplica una función a `this` y regresa el resultado de esa función.  Resulta útil para aplicar funciones encadenadas.
 
 Ejemplo Básico:
 ```
 5.pipe({|n| 2*n}).pipe({|n| [n]})// [10]
 ```

 Ejemplo de uso real:

```
//Permite transformar esto
(
var melodía = ~concat.(//concatena la ~melodiaEnNodos -- e.g. [["B4"], ["C5", "Bb6"]] -> ["B4", "C5", "Bb6"]
	~melodiaEnNodos 
		.collect(_.namemidi)
		.collect(_.midicps)
);

~taskMaker.(melodía,\miSynthdef).play //inyecta la melodia junto con un SynthDef a una función que genera un Task 
)

//en esto
(
~melodiaEnNodos
	.collect(_.namemidi) 
	.collect(_.midicps) 
	.pipe(~concat.(_)) // hasta aquí lo que arriba es la variable "melodía"
	.pipe(~taskMaker.(_, \miSynthdef)) //inyecta la melodia junto con un SynthDef a una función que genera un Task 
	.play 
)
```