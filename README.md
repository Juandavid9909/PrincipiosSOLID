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