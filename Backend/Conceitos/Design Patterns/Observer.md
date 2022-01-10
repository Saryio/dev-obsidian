# Observer #design/pattern
## **Observer** é um padrão de design de código que permite observar o estado de uma classe e atualizar se quiser o próprio estado.
![Observer](../../../resources/observer.png)

#### Exemplo com Weather Station
### Primeiro declaramos a interface de quem será observado e do observador respectivamente:

```typescript
	interface Subject {
		registerObserver(o: Observer): void
		removeObserver(o: Observer): void
		notifyObservers(): void
	}

	interface Observer{
		update(temperature: number): void
	}
```

### Após isso criamos a classe Weather Station, implementando a interface Subject:
### Repare que ao setar uma nova temperatura, os observadores que forem adicionados ao array observers serão notificados:

```typescript
	class WeatherStation implements Subject{
	
		private temperature = 20
		private observers: Observer[] = []
		
		setTemperature(temperature: number){
			this.temperature = temperature
			console.log("Temperatura é: " + this.temperature)
			this.notifyObservers()
		}
		
		registerObserver(o: Observer): void {
			this.observers.push(o)
		}
		
		removeObserver(o: Observer): void {
			let index = this.observers.indexOf(o)
			this.observers.splice(index, 1)
		}
		
		notifyObservers(): void {
			this.observers.forEach(observer=>{
				observer.update(this.temperature)
			})
		}
	}
```

### Criamos a classe Fan que é um observador de WeatherStation
### Repare que no construtor ele recebe como parâmetro o objeto que será observado e passa a si próprio como parâmetro para o registerObserver da classe WeatherStation:

```typescript
	class Fan implements Observer{

		private subject: Subject
		
		constructor(weatherStation: Subject){
			this.subject = weatherStation
			weatherStation.registerObserver(this)
		}
		
		update(temperature: number): void {
			if(temperature > 30){
				console.log("\nLigando ventoinhas")
			}else{
				console.log("\nVentoinhas desligadas");
			}
		}
	}
```

### Instanciando as classes weatherStation() e Fan(weatherStation), vemos como acontece o comportamento de Fan quando alteramos algum valor de WeatherStation: 

```typescript
	const weatherStation = new WeatherStation()
	const fan = new Fan(weatherStation)
```

![resultado 1](../../../resources/observable_1.png)

```typescript
	weatherStation.setTemperature(65)
```

![resultado 2](../../../resources/observable_2.png)

```typescript
	weatherStation.setTemperature(16)
```