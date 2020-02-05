# JSX
Se llama JSX, y es una extensión de la sintaxis de JavaScript. Recomendamos usarlo con React para describir cómo debería ser la interfaz de usuario. JSX puede recordarte a un lenguaje de plantillas, pero viene con todo el poder de JavaScript.

<iframe width="560" height="315" src="https://www.youtube.com/embed/TKHrZ3AItHY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

```js
const element = <h1>Hello, world!</h1>;
```
Esta curiosa sintaxis de etiquetas no es ni un string ni HTML, Se llama JSX.

Conoce más en la guía oficial [https://es.reactjs.org/docs/introducing-jsx.html](https://es.reactjs.org/docs/introducing-jsx.html)

## Insertando
Podemos insertar Javascript dentro de expresiones JSX como por ejemplo:

```js
import React from 'react';

const JsxAccion = () => {

    const saludo = 'Soy una constante!'

    return (
        <h1>Hola! {saludo}</h1>
    );
}
 
export default JsxAccion;
```
Fíjate que utilizamos las `{}` para llamar a una constante, tu puedes utilizar dentro de estas llaves código JS!

```js
import React, {Fragment} from 'react';

const JsxAccion = () => {

    const temperatura = 21;

    return (
        <Fragment>
            <h2>Frío o Calor?</h2>
            <p>
                {
                    temperatura > 20 ? 'Calor!' : 'Frio!'
                }
            </p>
        </Fragment>
    );
}

export default JsxAccion;
```
Ahora en este ejemplo estamos mezclando con un operador ternario (Atajo de condicional if)

```js
const element = <img src={user.avatarUrl}></img>;
```
También lo puedes utilizar en atributos.

:::warning
No pongas comillas rodeando llaves cuando insertes una expresión JavaScript en un atributo. Debes utilizar comillas (para los valores de los strings) o llaves (para las expresiones), pero no ambas en el mismo atributo.
:::

## Listas y Keys
[https://es.reactjs.org/docs/lists-and-keys.html](https://es.reactjs.org/docs/lists-and-keys.html)
Se utiliza la función `map()` para pintar un Array.

```js
import React,{Fragment, useState} from 'react';

const Listas = () => {

    const [numeros, setNumero] = useState([1,2,3,4,5,6])

    return (
        <Fragment>
            <ul>
                {
                    numeros.map((item, index) => 
                        <li key={index}>
                            {item} - {index}
                        </li>
                    )
                }
            </ul>
        </Fragment>
    );
}
 
export default Listas;
```
Cuando ejecutes este código, serás advertido que una key debería ser proporcionada para ítems de lista. Una “key” es un atributo especial string que debes incluir al crear listas de elementos.

## Jugando
```js
import React,{Fragment, useState} from 'react';

const Listas = () => {

    const [numeros, setNumero] = useState([1,2,3,4,5,6])

    const [tiempo, setTiempo] = useState(1)

    const aumentar = () => {
        setTiempo(tiempo + 1)
        setNumero([
            ...numeros,
            tiempo + 6
        ])
    }

    return (
        <Fragment>
            <ul>
                <button onClick={aumentar}>Aumentar</button>
                <p>Tiempo: {tiempo}</p>
                {
                    numeros.map((item, index) => 
                        <li key={index}>
                            {item} - {index}
                        </li>
                    )
                }
            </ul>
        </Fragment>
    );
}
 
export default Listas;
```

## Operador de propagacion
[http://www.etnassoft.com/2014/06/03/el-operador-de-propagacion-en-javascript-ecmascript-6-y-polyfill/](http://www.etnassoft.com/2014/06/03/el-operador-de-propagacion-en-javascript-ecmascript-6-y-polyfill/)

Concatenar Array
```js
const arrayUno = ['Chile', 'Argentina']
const arrayDos = ['Perú', 'Mexico']

const Unidos = [...arrayUno, ...arrayDos]
console.log(Unidos)
```

