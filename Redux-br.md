# REDUX

É um container de estado previsivel para aplicações javascript

## Actions

### O que são?

Descrições de uma ação de como o estado será modificado

#### Exemplo:

```javascript
{
	type: 'ADD_TODO',
	payload: {
		text: 'Learn Redux',
		completed: false
	}
}
```

- Uma *Action* tem um **type** que descreve a ação que está sendo executada.
- Uma *Action* tem um **payload** que é o valor da action em sí
- Por serem ***Objetos*** podem ser logados, serializados, e re-executados.

## Reducers

### O que são?

São **funções puras** que recebem o estado *atual*, a *action* e retornam o *estado* modificado de acordo com a action.

```(state, action) => state```

#### Exemplo:

```javascript
function todos(state = [], action){
	switch(action.type){
		case 'ADD_TODO':
			return [
				...state,
				{
					text: action.text,
					completed: false
				}
			]
		default:
			return state
	}
}
```

- *Reducers* nunca devem mutar o estado, ao contrário, devem sempre retornar uma cópia do estado quando o mesmo for alterado.

- Como *Reducers* são apenas funções puras, que dependem de um estado inicial e uma action, testa-los se torna simples.

```javascript
const actions = [
	{
		type: 'ADD_TODO',
		payload: {
			text: 'Learn Redux',
			completed: false
		}
	}
]

const state = actions.reduce(todos, [])
expect(state.length).equal(1)
```

## Store

Aplicações *Redux* possuem uma única *Store*. E são criadas da seguinte maneira:

```javascript
import { createStore } from 'redux'

const store = createStore(reducer)
```

- Cada **Store** recebe apenas um único *reducer*, mas como *reducers* são funções você pode combina-los da maneira que quiser.

#### Combine reducers

```javascript
import { combineReducers } from 'redux'

const reducer = combineReducers({
	reducer1: (state, action) => state,
	reducer2: (state, action) => state
})
```
- A *store* possui três métodos: **dispatch**, **getState** e **subscribe**.

### dispatch

Serve para comunicar *actions* para a store:

```javascript
store.dispatch({
	type: 'ADD_TODO',
	payload: {
		text: 'Learn Redux',
		completed: false
	}
})
```
### getState

Consulta todo o estado da aplicação em um determinado momento:

```javascript
store.getState()

/*
{
	visibilityFilter: 'SHOW_ALL',
	todos: [
		{
			text: 'Learn Redux',
			completed: true
		},
		{
			text: 'Drink beer',
			completed: false
		}
	]
}
*/
```

### subscribe

Registra uma callback para todo momento em que um novo estado é gerado à partir de uma nova action.

```javascript
store.subscribe(() => {
	console.log(store.getState())
})
```

## Middleware

Função que transformam as action antes de passar elas para o reducer da sua aplicação.
Utilizado para converter actions assincronas em sincronas.

# Referências

[Redux é um container de estado - RSJS](https://www.youtube.com/watch?v=pFLglnx3zBw)
