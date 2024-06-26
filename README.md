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

```typescript
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

```typescript
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


# Principios SOLID

Los principios SOLID nos indican cómo organizar nuestras funciones y estructuras de datos en componentes y cómo dichos componentes deben estar interconectados. A pesar de que suele estar enfocado en las clases, también puede ser utilizado en los módulos, etc.


## Acrónimo SOLID

- **S**ingle Responsibility: Responsabilidad única.
- **O**pen and Close: Abierto y cerrado.
- **L**iskov Substitution: Sustitución de Liskov.
- **I**nterface segregation: Segregación de interfaz.
- **D**ependency inversion: Inversión de dependencias.

Importante recordar que son principios, no reglas. Las reglas son obligatorias, los principios son recomendaciones que nos ayudarán a tener un mejor código.


## SRP - Principio de responsabilidad única

*"Nunca debería haber más de un motivo por el cual cambiar una clase o un módulo." - __Robert C. Martin__*.

Importante tener claro que tener una única responsabilidad no significa hacer una única cosa. Se trata de diseñar componentes que sólo estén expuestos a una fuente de cambio.

### Ejemplo

```typescript
// Sin principio SRP
(()  => {
	interface Product {
		id: number;
		name: string;
	}

	// Usualmente, esto es una clase para controlar la vista que es desplegada al usuario
	// Recuerden que podemos tener muchas vistas que realicen este mismo trabajo.
	class  ProductBloc {

		loadProduct(id: number) {
			// Realiza un proceso para obtener el producto y retornarlo
			console.log('Producto: ',{ id, name: 'OLED Tv' });
		}

		saveProduct(product: Product) {
			// Realiza una petición para salvar en base de datos
			console.log('Guardando en base de datos', product );
		}

		notifyClients() {
			console.log('Enviando correo a los clientes');
		}

		onAddToCart(  productId: number ) {
			// Agregar al carrito de compras
			console.log('Agregando al carrito ', productId );
		}
	}

	const  productBloc  =  new  ProductBloc();

	productBloc.loadProduct(10);
	productBloc.saveProduct({ id: 10, name: 'OLED TV' });
	productBloc.notifyClients();
	productBloc.onAddToCart(10);
})();


// Con principio SRP
(()  => {
	interface Product {
		id: number;
		name: string;
	}

	class  ProductService {

		getProduct(id: number) {
			console.log('Producto: ',{ id, name: 'OLED Tv' });
		}

		saveProduct(product: Product) {
			console.log('Guardando en base de datos', product );
		}
	}

	class  Mailer {

		private  masterEmail: string =  "juandavid@mail.com";

		sendEmail(emailList: string[], template:  "to-clients"  |  "to-admins") {
			console.log('Enviando correo a los clientes', template);
		}
	}

	// Usualmente, esto es una clase para controlar la vista que es desplegada al usuario
	// Recuerden que podemos tener muchas vistas que realicen este mismo trabajo.
	class  ProductBloc {

		private  productService: ProductService;
		private  mailer: Mailer;

		constructor(productService: ProductService, mailer: Mailer) {
			this.productService  =  productService;
			this.mailer  =  mailer;
		}

		loadProduct(id: number) {
			this.productService.getProduct(id);
		}

		saveProduct(product: Product) {
			this.productService.saveProduct(product);
		}

		notifyClients() {
			this.mailer.sendEmail(["eduardo@google.com"], "to-clients");
		}
	}

	class  CartBloc {

		private  itemsInCart: Object[] = [];

		addToCart(productId: number) {
			console.log('Agregando al carrito ', productId );
		}
	}

	const  productService  =  new  ProductService();
	const  mailer  =  new  Mailer();
	const  productBloc  =  new  ProductBloc(productService, mailer);
	const  cartBloc  =  new  CartBloc();

	productBloc.loadProduct(10);
	productBloc.saveProduct({ id: 10, name: 'OLED TV' });
	productBloc.notifyClients();
	cartBloc.addToCart(10);
})();
```

### Detectar incumplimiento de SRP
- Nombres de clases y módulos demasiado genéricos. Esto termina haciendo que esta clase y/o módulo tenga demasiadas responsabilidades.
- Cambios en el código suelen afectar la clase o módulo.
- La clase involucra múltiples capas (almacenamiento, comunicación con la base de datos, capa para interfaz de usuario).
- Número elevado de importaciones.
- Cantidad elevada de métodos públicos.
- Excesivo número de líneas de código.


## OCP - Principio de abierto y cerrado

Es un principio que depende mucho del contexto. Establece que las entidades de software (clases, módulos, métodos, etc) deben estar abiertas para la extensión, pero cerradas para la modificación.

La forma más sencilla de demostrar este principio es considerar un método que hace una cosa. Digamos que tenemos que grabar o escribir en un archivo de texto, y para ello tenemos una función, y de repente llegan nuevos requisitos, ahora ya el archivo no se llamará `hola.txt` sino `adios.txt`. Al tener que entrar a nuestro método a configurar el nombre del archivo estaremos violando este principio.

La forma en la que podríamos solventar esta situación sería crear un método en el que se reciba el nombre del archivo, y no importaría el nombre del archivo que necesitemos, ya que nuestra clase no se verá modificada y es tolerante al cambio.

Este principio también se puede lograr de muchas maneras, incluso mediante el uso de la herencia o mediante patrones de diseño de composición como el patrón de estrategia.

### Ejemplo
```javascript
// Archivo main
import { PhotosService, PostService, TodoService } from  './02-open-close-b';

(async  ()  => {

	const todoService = new TodoService();
	const postService = new PostService();
	const photosService = new PhotosService();

	const todos = await todoService.getTodoItems();
	const posts = await postService.getPosts();
	const photos = await photosService.getPhotos();

	console.log({ todos, posts, photos });
})();

// Archivo auxiliar
// Hay que agregar la dependencia de axios ```yarn add axios```
import  axios  from  'axios';

export  class  TodoService {

	async  getTodoItems() {
		const { data } =  await  axios.get('https://jsonplaceholder.typicode.com/todos/');

		return  data;
	}
}

export  class  PostService {

	async  getPosts() {
		const { data } =  await  axios.get('https://jsonplaceholder.typicode.com/posts');

		return  data;
	}
}

export  class  PhotosService {

	async  getPhotos() {
		const { data } =  await  axios.get('https://jsonplaceholder.typicode.com/photos');

		return  data;
	}
}
```

Como podemos ver, la clase de servicio tiene todas las responsabilidades, ya que pueden cambiar las URLs o la forma en las que se ejecutan los llamados en Axios, así que se pueden generar modificaciones y violar el principio.

```typescript
// Archivo main
import { PhotosService, PostService, TodoService } from './02-open-close-b';

(async ()  => {

	const httpClient = new HttpClient();

	const todoService = new TodoService(httpClient);
	const postService = new PostService(httpClient);
	const photosService = new PhotosService(httpClient);

	const todos = await todoService.getTodoItems();
	const posts = await postService.getPosts();
	const photos = await photosService.getPhotos();

	console.log({ todos, posts, photos });
})();

// Archivo auxiliar
import { HttpClient } from  "./03-open-close-c";

export  class  TodoService {

	async  getTodoItems() {
		const { data } =  await  this.http.get('https://jsonplaceholder.typicode.com/todos/');

		return  data;
	}
}

export  class  PostService {

	async  getPosts() {
		const { data } =  await  this.http.get('https://jsonplaceholder.typicode.com/posts');

		return  data;
	}
}

export  class  PhotosService {

	async  getPhotos() {
		const { data } =  await  this.http.get('https://jsonplaceholder.typicode.com/photos');

		return  data;
	}
}

// Nueva clase
import  axios  from  "axios";

export  class  HttpClient {

	async  get(url: string) {
		const { data, status } =  await  axios.get(url);

		return { data, status };
	}
}

// Nueva clase removiendo Axios
// import  axios  from  "axios";

export  class  HttpClient {

	// async get(url: string) {
		// const { data, status } = await axios.get(url);

		// return { data, status };
	// }
	
	async  get(url: string) {
		const  resp  =  await  fetch(url);
		const  data  =  await  resp.json();

		return { data, status: resp.status };
	}
}
```

### Detectar incumplimiento de OCP
- Cambios normalmente afectan nuestra clase o módulo.
- Cuando una clase o módulo afecta muchas capas (presentación, almacenamiento, etc).


## Principio de Substitución de Liskov

*"Las funciones que utilicen punteros o referencias a clases base deben ser capaces de usar objetos de clases derivadas sin saberlo." - __Robert C. Martin__*.

Siendo U un subtipo de T, cualquier instancia de T debería poder ser sustituida por cualquier instancia de U sin alterar las propiedades del sistema.

### Ejemplo
```typescript
// Archivo main
import { Tesla, Audi, Toyota, Honda } from  './03-liskov-b';

(()  => {
	const  printCarSeats  =  (  cars: (Tesla | Audi | Toyota | Honda)[] )  => {

	for (const  car  of  cars) {
		if( car  instanceof Tesla ) {
			console.log( 'Tesla', car.getNumberOfTeslaSeats() )
			continue;
		}

		if( car  instanceof Audi ) {
			console.log( 'Audi', car.getNumberOfAudiSeats() )
			continue;
		}

		if( car  instanceof Toyota ) {
			console.log( 'Toyota', car.getNumberOfToyotaSeats() )
			continue;
		}

		if( car  instanceof Honda ) {
			console.log( 'Honda', car.getNumberOfHondaSeats() )
			continue;
		}
	}	
}

const  cars  = [
	new  Tesla(7),
	new  Audi(2),
	new  Toyota(5),
	new  Honda(5),
];

printCarSeats( cars );
})();

// Archivo extra
export  class  Tesla {

	constructor(  private  numberOfSeats: number ) {}

	getNumberOfTeslaSeats() {
		return  this.numberOfSeats;
	}
}

export  class  Audi {

	constructor(  private  numberOfSeats: number ) {}

	getNumberOfAudiSeats() {
		return  this.numberOfSeats;
	}
}

export  class  Toyota {

	constructor(  private  numberOfSeats: number ) {}

	getNumberOfToyotaSeats() {
		return  this.numberOfSeats;
	}
}

export  class  Honda {

	constructor(  private  numberOfSeats: number ) {}

	getNumberOfHondaSeats() {
		return  this.numberOfSeats;
	}
}
```

Para agregar una nueva marca de carro se modificarían muchas cosas, además de que tocaría crear la nueva clase repitiendo el mismo método que en las demás.

```typescript
// Archivo main
import { Tesla, Audi, Toyota, Honda, Vehicle } from  './03-liskov-b';

(()  => {
	const  printCarSeats  =  (  cars: (Tesla | Audi | Toyota | Honda)[] )  => {

	cars.forEach((car)  => {
		console.log(car.constructor.name, car.getNumberOfSeats());
	});	
}

const  cars  = [
	new  Tesla(7),
	new  Audi(2),
	new  Toyota(5),
	new  Honda(5),
];

printCarSeats( cars );
})();

// Archivo extra
export  abstract  class  Vehicle {

	abstract  getNumberOfSeats(): number;
}

export  class  Tesla  extends  Vehicle {

	constructor(  private  numberOfSeats: number ) {
		super();
	}

	getNumberOfSeats() {
		return  this.numberOfSeats;
	}
}

export  class  Audi  extends  Vehicle {

	constructor(  private  numberOfSeats: number ) {
		super();
	}

	getNumberOfSeats() {
		return  this.numberOfSeats;
	}
}

export  class  Toyota  extends  Vehicle {

	constructor(  private  numberOfSeats: number ) {
		super();
	}

	getNumberOfSeats() {
		return  this.numberOfSeats;
	}
}

export  class  Honda  extends  Vehicle {

	constructor(  private  numberOfSeats: number ) {
		super();
	}

	getNumberOfSeats() {
		return  this.numberOfSeats;
	}
}
```


## Principio de segregación de interfaz

*"Los clientes no deberían estar obligados a depender de interfaces que no utilicen." - __Robert C. Martin__*.

### Ejemplo
```typescript
interface Bird {
	fly(): void;
	eat(): void;
	run(): void;
}

class  Tucan  implements  Bird {

	public  fly() {}

	public  eat() {}

	public  run() {}
}

class  Humminbird implements  Bird {

	public  fly() {}

	public  eat() {}

	public  run() {}
}

class  Ostrich  implements  Bird {

	public  fly() {
		throw  new  Error("Esta ave no vuela");
	}

	public  eat() {}

	public  run() {}
}

class  Penguin  implements  Bird {

	public  fly() {
		throw  new  Error("Esta ave no vuela");
	}

	public  eat() {}

	public  run() {}

	public  swim() {}
}
```

Como podemos ver, al implementar la interfaz en nuestras clases tenemos como inconveniente que por ejemplo para el Avestruz se debe implementar el método `fly` a pesar de que las mismas no vuelan, otro ejemplo es la clase Penguin ya que estos también nadan, y al agregar el método a la clase estamos incumpliendo con la interfaz ya que o tendríamos que quitar el método swim, o tendríamos que agregar el método en todas las clases que implementen la interfaz. Esto es una clara violación a nuestro principio de segregación de interfaz.

```typescript
interface Bird {
	eat(): void;
}

interface FlyingBird {
	fly(): void;
}

interface RunningBird {
	run(): void;
}

interface SwimmerBird {
	swim(): void;
}

class  Tucan  implements  Bird, FlyingBird {

	public  fly() {}

	public  eat() {}
}

class  Humminbird  implements  Bird, FlyingBird {

	public  fly() {}

	public  eat() {}
}

class  Ostrich  implements  Bird, RunningBird {

	public  eat() {}

	public  run() {}
}

class  Penguin  implements  Bird, SwimmerBird {

	public  eat() {}

	public  run() {}

	public  swim() {}
}
```

### Detectar incumplimiento de ISP
- Si las interfaces que diseñamos nos obligan a violar los principios de responsabilidad única y substitución de Liskov.


## Principio de inversión de dependencias

*"Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones. Las abstracciones no deben depender de concreciones. Los detalles deben depender de abstracciones." - __Robert C. Martin__*.

- Los módulos de alto nivel no deberían depender de módulos de bajo nivel.
- Ambos deberían depender de abstracciones.
- Las abstracciones no deberían depender de detalles.
- Los detalles deberían depender de abstracciones.

Los componentes más importantes son aquellos centrados en resolver el problema subyacente al negocio, es decir, la capa de dominio.

Los menos importantes son los que están próximos a la infraestructura, es decir, aquellos relacionados con la UI, la persistencia, la comunicación con APIs externas, etc.

Depender de abstracciones se refiere a clases abstractas o interfaces. Uno de los motivos más importantes por el cual las reglas de negocio o capa de dominio deben depender de estas y no de concreciones es que aumenta su tolerancia al cambio.

### ¿Por qué obtenemos este beneficio?
- Cada cambio en un componente abstracto implica un cambio en su implementación.
- Por el contrario, los cambios en implementaciones concretas, la mayoría de veces, no requieren cambios en las interfaces que implementa.

### Inyección de dependencias
Dependencia en programación, significa que un módulo o componente requiere de otro para poder realizar su trabajo.

En algún momento nuestro programa o aplicación llegará a estar formado por muchos módulos. Cuando esto pase, es cuando debemos usar inyección de dependencias.

### Ejemplo
```typescript
// Sin inyección de dependencias
class UseCase {
	constructor() {
		this.externalService = new ExternalService();
	}

	doSomething() {
		this.externalService.doExternalTask();
	}
}

class ExternalService {
	doExternalTask() {
		console.log("Doing task...);
	}
}

// Con inyección de dependencias
class UseCase {
	constructor(externalService: ExternalService) {
		this.externalService = externalService;
	}

	doSomething() {
		this.externalService.doExternalTask();
	}
}

class ExternalService {
	doExternalTask() {
		console.log("Doing task...);
	}
}
```