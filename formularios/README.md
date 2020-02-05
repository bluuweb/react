# Formularios
Documentación oficial: [https://es.reactjs.org/docs/forms.html](https://es.reactjs.org/docs/forms.html)

```js
import React, {Fragment, useState} from 'react';

const Formulario = () => {


    const [datos, setDatos] = useState({
        nombre: '',
        apellido: ''
    })

    const handleInputChange = (event) => {
        // console.log(event.target.name)
        // console.log(event.target.value)
        setDatos({
            ...datos,
            [event.target.name] : event.target.value
        })
    }

    const enviarDatos = (event) => {
        event.preventDefault()
        console.log('enviando datos...' + datos.nombre + ' ' + datos.apellido)
    }

    return (
        <Fragment>
            <h1>Formulario</h1>
            <form className="row" onSubmit={enviarDatos}>
                <div className="col-md-3">
                    <input type="text" placeholder="Nombre" className="form-control" onChange={handleInputChange} name="nombre"></input>
                </div>
                <div className="col-md-3">
                    <input type="text" placeholder="Apellido" className="form-control" onChange={handleInputChange} name="apellido"></input>
                </div>
                <button type="submit" className="btn btn-primary">Enviar</button>
            </form>
            <ul>
                <li>{datos.nombre}</li>
                <li>{datos.apellido}</li>
            </ul>
        </Fragment>
    );
}
 
export default Formulario;
```

## State
Los datos que utilizaremos en nuestro formulario:

```js
const [datos, setDatos] = useState({
    nombre: '',
    apellido: ''
})
```

## Form
Utilizando clases de Bootstrap para que se vea más bonito, atributos y eventos para que la magia funcione:

```html
<form className="row" onSubmit={enviarDatos}>
    <div className="col-md-3">
        <input 
            type="text" 
            placeholder="Nombre" 
            className="form-control" 
            onChange={handleInputChange} 
            name="nombre" />
    </div>
    <div className="col-md-3">
        <input 
            type="text" 
            placeholder="Apellido" 
            className="form-control" 
            onChange={handleInputChange} 
            name="apellido" />
    </div>
    <button type="submit" className="btn btn-primary">Enviar</button>
</form>
```

## Evento onChange
Estará al pendiente de los cambios que se registren en nuestro input, por lo tanto creamos una función para modificar nuestro state.

```js
const handleInputChange = (event) => {
    // console.log(event.target.name)
    // console.log(event.target.value)
    setDatos({
        ...datos,
        [event.target.name] : event.target.value
    })
}
```

A partir de ECMAScript 2015, la sintaxis del inicializador de objetos también admite nombres de propiedades calculados. Eso le permite poner una expresión entre paréntesis [], que se calculará y usará como el nombre de la propiedad. [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Computed_property_names](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Computed_property_names)

## onSubmit
Ahora con los datos ya ingresados podemos utilizar el evento onSubmit para procesar el formulario:

```html
<form onSubmit={enviarDatos}>
```

```js
const enviarDatos = (event) => {
    event.preventDefault()
    console.log('enviando datos...' + datos.nombre + ' ' + datos.apellido)
}
```


