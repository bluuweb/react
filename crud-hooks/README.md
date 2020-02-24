# CRUD React Hooks
No vamos a reinventar la rueda por lo tanto nos basaremos en el siguiente ejemplo: [https://www.taniarascia.com/crud-app-in-react-with-hooks/](https://www.taniarascia.com/crud-app-in-react-with-hooks/)

::: warning Modificaremos las secciones de: 
- Generar ID
- Form Agregar usuario
- Form Editar usuario
:::
El código completo aquí: [https://github.com/bluuweb/crud-react-user](https://github.com/bluuweb/crud-react-user)

## Configuraciones iniciales
Ya hemos visto que para crear una App con React podemos utilizar el siguiente código:

```
npx create-react-app react-hooks
```

Elimina todos los archivos a excepción de:

```
app.js
index.css
index.js
```

## Instalaciones adicionales

[https://react-hook-form.com/get-started](https://react-hook-form.com/get-started)
```
npm install react-hook-form
```

[https://www.npmjs.com/package/uuid](https://www.npmjs.com/package/uuid)
```
npm install uuid
```

## index.js
Déjalo como este:
```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

## index.css
Copia y pega lo siguiente: [https://taniarascia.github.io/primitive/css/main.css](https://taniarascia.github.io/primitive/css/main.css)

## App.js
Ahora seguiremos el tutorial antes descrito pero modificando las secciones de: generar id, agregar usuario y editar (utilizaremos React Hook Form, tambien visto en los videos anteriores)

## Agregar usuario
```js
import React from 'react';
import { useForm } from 'react-hook-form'

const AddUserForm = (props) => {

    const {register, errors, handleSubmit} = useForm();

    const onSubmit = (data, e) => {
        data.id = null
        console.log(data)
        props.addUser(data)
        e.target.reset();
    }

    return (
        <form onSubmit={handleSubmit(onSubmit)}>
            <label>Name</label>
            <input 
                type="text" 
                name="name"
                ref={register({required: {value: true, message: 'Valor requerido'}})}
                />
            <div>
                {errors?.name?.message}
            </div>
            <label>Username</label>
            <input 
                type="text" 
                name="username" 
                ref={register({required: {value: true, message: 'Valor requerido'}})}
                />
            <div>
                {errors?.username?.message}
            </div>
            <button type="submit">Add new user</button>
        </form>
    );
}
 
export default AddUserForm;
```

## Editar usuario
App.js
```js
import React, {useState} from 'react';
import UserTable from './components/UserTable';
import AddUserForm from './components/AddUserForm';
import EditYo from './components/EditYo';
import { v4 as uuidv4 } from 'uuid';

function App() {

  // Agregar usuarios
  const usersData = [
    { id: uuidv4(), name: 'Tania', username: 'floppydiskette' },
    { id: uuidv4(), name: 'Craig', username: 'siliconeidolon' },
    { id: uuidv4(), name: 'Ben', username: 'benisphere' },
  ]

  const [users, setUsers] = useState(usersData)

  const addUser = (user) => {
    user.id = uuidv4()
    console.log(user)
    setUsers([
      ...users,
      user
    ])
  }

  // Eliminar usuario
  const deleteUser = id => {
    setUsers(users.filter(user => user.id !== id))
  }

  // Editar usuario
  const [editing, setEditing] = useState(false)

  const initialFormState = { id: null, name: '', username: '' }
  const [currentUser, setCurrentUser] = useState(initialFormState)

  const editRow = user => {
    setEditing(true) 
    setCurrentUser({ id: user.id, name: user.name, username: user.username })
  }

  const updateUser = (id, updatedUser) => {
    setEditing(false)
    setUsers(users.map(user => (user.id === id ? updatedUser : user)))
  }

  return (
    <div className="container">
      <h1>CRUD App with Hooks</h1>
      <div className="flex-row">
        <div className="flex-large">
        {editing ? (
          <div>
            <h2>Edit user</h2>
            <EditYo 
              setEditing={setEditing}
              currentUser={currentUser}
              updateUser={updateUser}
            />
          </div>
        ) : (
          <div>
            <h2>Add user</h2>
            <AddUserForm addUser={addUser}  />
          </div>
        )}
      </div>
        <div className="flex-large">
          <h2>View users</h2>
          <UserTable users={users} deleteUser={deleteUser} editRow={editRow} />
        </div>
      </div>
    </div>
  );
}

export default App;
```

EditUserForm.jsx
```js
import React from 'react'
import { useForm } from 'react-hook-form'

const EditYo = (props) => {

    const {register, errors, handleSubmit, setValue} = useForm({
        defaultValues: props.currentUser
    });

    setValue('name', props.currentUser.name)
    setValue('username', props.currentUser.username)

    const onSubmit = (data, e) => {
        data.id = props.currentUser.id
        console.log(data)
        props.updateUser(props.currentUser.id, data)
        e.target.reset()
    }

    return (
        <form onSubmit={handleSubmit(onSubmit)}>
            <label>Name</label>
            <input 
                type="text" 
                name="name"
                ref={register({required: {value: true, message: 'Valor requerido'}})}
                />
            <div>
                {errors?.name?.message}
            </div>
            <label>Username</label>
            <input 
                type="text" 
                name="username" 
                ref={register({required: {value: true, message: 'Valor requerido'}})}
                />
            <div>
                {errors?.username?.message}
            </div>
            <button type="submit">Edit user</button>
            <button onClick={() => props.setEditing(false)} className="button muted-button">
                Cancel
            </button>
        </form>
    );
}
 
export default EditYo;
```

