
# S.O.L.I.D. #BoasPraticas

## Conjunto de princípios da POO

# S - Single Responsibility Principle
##### *"Uma classe deve ter apenas um motivo para mudar"*
### Esse princípio trata da coesão das classes, ou seja, que suas funcionalidades sejam específicas para a classe.
```javascript
errado:
	class Aluno{
		ler(){}
		escrever(){}
		conectarDB(){} <--- função deve ser de outra classe
	}
```
	
```javascript
melhor:
	class Aluno{
		nota: number
		getNota: ()=>{}
		setNota: ()=>{}
		
		ler(){}
		escrever(){}
		perguntar(){}
	}
```

# O - Open-Closed Principle
#####  *"As entidades de software (classes, módulos, funções etc.) devem ser abertas para ampliação, mas fechadas para serem modificadas"*. 
### De curto e grosso modo, entidades de software que seguem esse princípio não devem ser modificadas com alterações no código fonte, apenas ampliadas, fazendo uso de interfaces, heranças e composições.

## L - Liskov Substitution Principle
##### Uma classe derivada deve ser substituível por sua classe base.
#