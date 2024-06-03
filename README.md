# Clean Code y deuda técnica

La deuda técnica es la falta de calidad en nuestro código, que genera una deuda que repercutirá en costos económicos, los cuales pueden ser:

- Tiempo en realizar mantenimientos.
- Tiempo en refactorizar código.
- Tiempo en comprender el código.
- Tiempo adicional en la transferencia del código.

Hay 4 tipos de deuda técnica:

- **Imprudente:** No hay tiempo, sólo copia y pega eso de nuevo.
- **Inadvertido:** ¿Qué son patrones de diseño?
- **Prudente:** Tenemos que entregar rápido, ya refactorizaremos.
- **Prudente e inadvertida:** Ahora sabemos cómo lo deberíamos haber hecho.


## Refactorización

Es simplemente un proceso que tiene como objetivo mejorar el código sin alterar su comportamiento para que sea más entendible y tolerante a cambios.

Usualmente para que una refactorización fuerte tenga el objetivo esperado, es imprescindible contar con pruebas automáticas.


## Clean Code

Es aquel que se ha escrito con la intención de que otra persona (o tú mismo en el futuro) lo entienda.

Nuestro código tiene que ser simple y directo, debería leerse con la misma facilidad que un texto bien escrito.


## Nombres pronunciables y expresivos

Escribir variables de forma adecuada para que el otro desarrollador tenga claro qué valor se guarda ahí.

```javascript
// Mal
const n = 53;

const tx = 0.15;

const cat = "T-Shirts";

const ddmmyyyy = new Date("Auguts 15, 1965 00:00:00");

// Bien
const numberOfUnits = 53;

const tax = 0.15;

const category = "T-Shirts";

const birthDate = new Date("Auguts 15, 1965 00:00:00");
```

También la ausencia de información técnica en nombres, la cual es más que todo la implementación que esa clase/interfaz está realizando, es decir que debemos procurar que sus nombres no tengan información técnica.

```javascript
// Mal
class AbstractUser {}

class UserMixin {}

class UserImplementation {}

interface UserInterface {}

// Bien
class User {}

interface User {}
```


## Nombres según el tipo de dato

Es una buena opción tener en los nombres de las variables algo que nos de una idea de qué tipo de dato contiene.

### Arreglos - Arrays
```javascript
// Malo
const fruit = ["manzana", "platano", "fresa"];

// Regular
const fruitList = ["manzana", "platano", "fresa"];

// Bueno
const fruits = ["manzana", "platano", "fresa"];

// Mejor
const fruitNames = ["manzana", "platano", "fresa"];
```

### Booleanos - Booleans
```javascript
// Mal
const open = true;
const write = true;
const fruit = true;
const active = false;
const noValues = true;
const notEmpty = true;

// Mejor
const isOpen = true;
const canWrite = true;
const hasFruit = true;
const isActive = false;
const hasValues = false;
const isEmpty = false;
```

### Números - Numbers
```javascript
// Mal
const fruits = 3;
const cars = 10;

// Mejor
const maxFruits = 5;
const minFruits = 1;
const totalFruits = 3;
const totalOfCars = 5;
```

### Funciones - Functions
Debemos ser claros en el nombre para indicar qué hace la función, pero también abstenerse de toda la implementación que hace la función.

```javascript
// Mal
createUserIfNotExists();
updateUserIfNotEmpty();
sendEmailIfFieldsValid();

// Mejor
createUser();
updateUser();
sendEmail();
```


## Consideraciones para las clases

Deben tener nombres formados por un sustantivo o frases de sustantivos, debemos evitar nombres genéricos porque estoy puede llevarnos a que las clases realicen más trabajo del que deberían.

- El nombre es lo más importante de la clase.
- Formados por un sustantivo o frases de sustantivo.
- No deben ser muy genéricos.
- Usar UpperCamelCase.

```javascript
// Malos
class Manager {}
class Data {}
class Info {}
class Individual {}
class Processor {}
class SpecialMonsterView {}

class SpecialViewingCaseMonsterManagerEventsHandlerActivitySingleton {}
```

### 3 preguntas para determinar si es un buen nombre
- ¿Qué hace exactamente la clase?
- ¿Cómo esta clase realiza exactamente cierta tarea?
- ¿Hay algo específico sobre su ubicación?

Si algo no tiene sentido, remuévelo o refactoriza, además tampoco se deben poner muchas palabras en el nombre de nuestra clase.


## Nombres de funciones, argumentos y parámetros

*"Sabemos que estamos desarrollando código limpio cuando cada función hace exactamente lo que su nombre indica.." - __Ward Cunningham__*.

```javascript
function sendEmail(toWhom: string): boolean {
	// Verificar correo
	if(!toWhom.includes("@")) return false;

	// Construir el cuerpo o mensaje

	// Enviar correo

	// Si todo sale bien
	return true;
}

function sendEmail(): boolean {
	// Verificar si el usuario existe

	// Revisar contraseña

	// Crear usuario en Base de datos

	// Si todo sale bien
	return true;
}
```

Es bueno limitar a 3 parámetros posicionales, para que no se vean muy aglomeradas.

```javascript
// No muy bien
function sendEmail(toWhom: string, from: string, body: string, subject: string, apiKey: string): boolean {}

// Bien
function sendEmail(toWhom: string, from: string, body: string): boolean {}

// Mejor
interface SendEmailOptions {
	toWhom: string;
	from: string;
	body: string;
	subject: string;
	apiKey: string;
}

function sendEmail({.toWhom, from, body, subject, apiKey }: SendEmailOptions): boolean {}
```

### Otras cosas a tener en cuenta
- Simplicidad es fundamental.
- Funciones de tamaño reducido.
- Funciones de una sola línea sin causar complejidad.
- Menos de 20 líneas.
- Evitar el uso del `else`.
- Prioriza el uso de la condicional ternaria.


## DRY (Don't repeat yourself)

*"Si quieres ser un programador productivo esfuérzate en escribir código legible." - __Robert C. Martin__*.

- Simplemente es evitar tener duplicidad en código.
- Simplifica las pruebas.
- Ayuda a centralizar procesos.
- Aplicar el principio DRY, usualmente lleva a refactorizar.


# Clean Code - Clases y Comentarios


## Estructura recomendada de una clase

*"El buen código parece estar escrito por alguien a quien le importa." -__Michael Feathers__*.

```typescript
class HtmlElement {
	public static domReady: boolean = false;

	private _id: string;
	private type: string;
	private updatedAt: number;

	static createInput(id: string) {
		return new HtmlElement(id, "input");
	}

	constructor(id: string, type: string) {
		this._id = id;
		this.type = type;
		this.updatedAt = Date.now();
	}

	setType(type: string) {
		this.type = type;
		this.updatedAt = Date.now();
	}

	get id(): string {
		return this.id;
	}
}
```

### Comenzar con lista de propiedades
1. Propiedades estáticas.
2. Propiedades públicas de último.

### Métodos
1. Empezando por los constructores estáticos.
2. Luego el constructor.
3. Seguidamente métodos estáticos.
4. Métodos privados después.
5. Resto de métodos de instancia ordenados de mayor a menor importancia.
6. Getters y Setters al final.


## Comentarios en el código

Evitar usar comentarios, pero cuando usamos librerías de terceros, APIs, frameworks, entre otras cosas, nos encontraremos ante situaciones en las que escribir un comentario será mejor que dejar una solución compleja o un hack sin explicación.

Los comentarios deberían de ser la excepción, no la regla.

*"No comentes el código mal escrito, reescríbelo". __Brian W. Kernighan__*.


## Uniformidad en el proyecto

Hay que procurar mantener siempre la misma nomenclatura en tanto nuestro sistema de archivos como los nombres de nuestras funciones, clases, etc. Por ejemplo si en nuestra carpeta de componentes tenemos otra carpeta para el componente product-list mientras que product-item está en la raíz, ya que lo correcto sería que ambos tengan el mismo nivel de sistema de archivos.


# Acrónimo STUPID

Son cosas que debemos evitar en nuestras aplicaciones, muchas veces pecamos de estos errores y es importante evitarlos.


## Code Smells

- **S**ingleton: Patrón singleton.
- **T**ight Coupling: Alto acomplamiento.
- **U**ntestability: Código no probable (unit test).
- **P**remature optimization: Optimizaciones prematuras.
- **I**ndescriptive Naming: Nombres poco descriptivos.
- **D**uplication: Duplicidad de código, no aplicar el principio DRY.

### Singleton
#### Ventajas
- Garantiza una única instancia de la clase a lo largo de toda la aplicación.

#### Desventajas
- Vive en el contexto global.
- Puede ser modificado por cualquiera y en cualquier momento.
- No es rastreable.
- Difícil de testear debido a su ubicación.

### Tight Coupling
Lo ideal es tener bajo acoplamiento y buena cohesión.

*"Queremos diseñar componentes que sean autocontenidos, autosuficientes e independientes. Con un objetivo y un propósito bien definido." - __The Pragmatic Programmer__*.

#### Desventajas
- Un cambio en un módulo por lo general provoca un efecto dominó de lo cambios en otros módulos.
- El ensamblaje de módulos puede requerir más esfuerzo y/o tiempo debido a la mayor dependencia entre módulos.
- Un módulo en particular puede ser más difícil de reutilizar y/o probar porque se deben incluir módulos independientes.

#### Posibles soluciones
- "A" tiene un atributo que se refiere a "B".
- "A" llama a los servicios de un objeto "B".
- "A" tiene un método que hace referencia a "B" (a través del tipo de retorno o parámetro).
- "A" es una subclase de (o implementa) la clase "B".

#### Cohesión
- La cohesión se refiere a lo que la clase (o módulo) puede hacer.
- La baja cohesión significaría que la clase realiza una gran variedad de acciones: Es amplia, no se enfoca en lo que debe hacer.
- Alta cohesión significa que la clase se enfoca en lo que debería estar haciendo, es decir, solo métodos relacionados con la intención de la clase.

#### Acoplamiento
Se refiere a cuán relacionadas o dependientes son dos clases o módulos entre sí.

- En bajo acoplamiento, cambiar algo importante en una clase no debería afectar a la otra.
- En alto acoplamiento, dificultaría el cambio y el mantenimiento de su código; dado que las clases están muy unidas, hacer un cambio podría requerir una renovación completa del sistema.

Un buen diseño de software tiene alta cohesión y bajo acoplamiento.

### Código no probable
- Código con alto acoplamiento.
- Código con muchas dependencias no inyectadas.
- Dependencias en el contexto global (tipo Singleton).

Debemos de tener en mente las pruebas desde la creación del código.

### Optimizaciones prematuras
Mantener abiertas las opciones retrasando la toma de decisiones nos permite darle mayor relevancia a lo que es más importante en una aplicación.

No debemos anticiparnos a los requisitos y desarrollar abstracciones innecesarias que puedan añadir una complejidad accidental.

#### Complejidad accidental
Cuando implementamos una solución compleja a la mínima indispensable.

#### Complejidad esencial
La complejidad es inherente al problema.

### Nombres poco descriptivos
- Nombres de variables mal nombradas.
- Nombres de clases genéricas.
- Nombres de funciones mal nombradas.
- Ser muy específico o demasiado genérico.

### Duplicidad de código
- Código es idéntico y cumple la misma función.
- Un cambio implicaría actualizar todo el código idéntico en varios lugares.
- Incrementa posibilidades de error humano al olvidad una parte para actualizar.


## Otros olores honoríficos

### Inflación
Cuando una parte del código (función, etc) está creciendo mucho, lo ideal es cortar o hacer más pequeño dicho método. Es decir, delegar ese método enorme en pequeños submétodos con tareas específicas que nos permita tener un código más legible y fácil de mantener.

### Obsesión primitiva
El uso de primitivos en lugar de objetos para manejar algunos datos. El uso de constantes para codificar cierta información. Esto es algo muy frecuente ya que usualmente podemos solucionar algo con sólo "1 espacio en memoria más". El tema es que esto puede ir creciendo y al final será una bola de nieve enorme.

Si se tienen una gran cantidad de variables primitivas, se puede crear una clase, función o módulo, para que tengamos todo centralizado y permitir la reutilización.