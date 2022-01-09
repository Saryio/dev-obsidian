
# S.O.L.I.D. #BoasPraticas

## Conjunto de princípios da POO

# S - Single Responsibility Principle
##### *"Uma classe deve ter apenas um motivo para mudar"*
## Esse princípio trata da coesão das classes, ou seja, que suas funcionalidades sejam específicas para a classe.
```javascript
errado:
	class Aluno{
		ler(){}
		escrever(){}
		conectarDB(){} //<--- função deve ser de outra classe
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
##### *"As entidades de software (classes, módulos, funções etc.) devem ser abertas para ampliação, mas fechadas para serem modificadas"*.
## De curto e grosso modo, entidades de software que seguem esse princípio não devem ser modificadas com alterações no código fonte, apenas ampliadas, fazendo uso de interfaces, heranças e composições.
```php
	ruim:
		class ContratoClt
		{
			public function salario()
			{
				/*...*/
			}
		}
			
		class Estagio
		{
			public function bolsaAuxilio()
			{
				/*...*/
			}
		}
			
		class FolhaDePagamento
		{
			protected $saldo;
		
			public function calcular($funcionario)
			{
				if ( $funcionario instanceof ContratoClt ) {

					$this->saldo = $funcionario->salario();

				} else if ( $funcionario instanceof Estagio) {
				
					$this->saldo = $funcionario->bolsaAuxilio();

				}
			}
	
		}
```

```php
	melhor:
		interface Remuneravel
		{
			public function remuneracao();
		}

		class ContratoClt implements Remuneravel
		{
			public function remuneracao()
			{
				/*...*/
			}
		}

		class Estagio implements Remuneravel
		{
			public function remuneracao()
			{
				/*...*/
			}
		
		}

		class FolhaDePagamento
		{
			protected $saldo;
		
			public function calcular(Remuneravel $funcionario)
			{
				$this->saldo = $funcionario->remuneracao();
			}

		}
```

# L - Liskov Substitution Principle
##### *"Uma classe derivada deve ser substituível por sua classe base."*
## Ou seja, quando novos comportamentos e recursos precisam ser adicionados no software, devemos estender e não alterar o código fonte original.

## Mesmo a herança sendo um mecanismo poderoso, ela deve ser utilizada de forma contextualizada e moderada, evitando os casos de classes serem estendidas apenas por possuírem algo em comum.
```php
	ruim:
	# - Sobrescrevendo um método que não faz nada...
	# - Um voluntário não tem remuneração, então nao deveria ser extendida por 
        #ContratoDeTrabalho
	class Voluntario extends ContratoDeTrabalho
	{
	
		public function remuneracao()
		{
		
		// não faz nada
		
		}
	
	}
	
	# - Lançando uma exceção inesperada...	
	class MusicPlay
	{
		public function play($file)
		
		{
		
			// toca a música
		
		}
	}
	
	class Mp3MusicPlay extends MusicPlay
	{
		public function play($file)
		{
			if (pathinfo($file, PATHINFO_EXTENSION) !== 'mp3') {
			
			throw new Exception;
			}
		// toca a música
		}
	}
	
	# - Retornando valores de tipos diferentes...
	class Auth
	{
		public function checkCredentials($login, $password)
		{
		// faz alguma coisa
			
			return true; # boolean
		}
	
	}
	
	class AuthApi extends Auth
	{
		public function checkCredentials($login, $password)
		{
		// faz alguma coisa
			return ['auth' => true, 'status' => 200]; # array relacional
		}
	}

```

```php
	na prática:

	class A
	{
		public function getNome()
		{
			echo 'Meu nome é A';
		}
	}

	class B extends A
	{
		public function getNome()
		{
			echo 'Meu nome é B';
		}
	}

	$objeto1 = new A;
	
	$objeto2 = new B;
	
	function imprimeNome(A $objeto)
	{
		return $objeto->getNome();
	}
	
	imprimeNome($objeto1); // Meu nome é A
	
	imprimeNome($objeto2); // Meu nome é B
	
```

# I - Liskov Substitution Principle
##### *"Uma classe derivada deve ser substituível por sua classe base."*
## Mesmo a herança sendo um mecanismo poderoso, ela deve ser utilizada de forma contextualizada e moderada, evitando os casos de classes serem estendidas apenas por possuírem algo em comum.