# Guia de estilo Swift

Esse guia de estilo é um produto de nossa equipe de desenvolvimento iOS. Reflete regras de programação em linguagem Swift que observamos serem eficientes no desenvolvimento de nossos projetos de aplicativos.

As diretrizes que aqui serão apresentadas encorajam práticas que buscam atingir as seguintes metas:

- Fazer com que seja  mais difícil escrever erros de programação, ou então facilitar a busca e correção dos erros

- Melhorar a organização tanto para facilitar a leitura quanto melhorar a clareza do conteúdo. Tendo em vista que um mesmo projeto pode ser desenvolvido por mais de uma pessoa e também pode ser revisado por outra pessoa

Alguns dos padrões que aqui podem ser observados podem opor os padrões seguidos pela comunidade Swift, porém ressaltamos que testamos e utilizamos essas práticas em nossa equipe e as mesmas se mostraram serem as mais eficientes até o presente momento.

Dito isso, esse é um documento que será atualizado constantemente, a medida que nossa equipe e a linguagem Swift evoluam, nossas práticas irão se adaptar acompanhando essas mudanças. Esse guia foi atualizado pela última vez em 4 de Maio de 2017.

## Sumário

- [Guia de estilo Swift](#guia-de-estilo-swift)
    - [1. Formatação de código](#1-formatação-de-código)
    - [2. Nomenclatura](#2-nomenclatura)
    - [3. Estilo de código](#3-estilo-de-código)
        - [3.1 Geral](#31-geral)
        - [3.2 Modificadores de acesso](#32-modificadores-de-acesso)
        - [3.3 Switch e Enum Statements](#33-switch-e-enum-statements)
        - [3.4 Opcionais](#34-opcionais)
        - [3.5 Protocols](#35-protocols)
        - [3.6 Propriedades](#36-properties)
        - [3.7 Closures](#37-closures)
        - [3.8 Arrays](#38-arrays)
        - [3.9 Lidando com erros](#39-lidando-com-erros)
        - [3.10 Usando `guard` Statements](#310-usando-guard-statements)
        - [3.11 Importando Bibliotecas](#311-importando-bibliotecas)
        - [3.12 Proteção contra Dynamic](#312-proteção-contra-dynamic)
        - [3.13 Uso do TODO](#313-uso-do-todo)
        - [3.14 Organização de Código](#314-organização-de-código)
        - [3.15 Boas Práticas](#314-boas-práticas)
    - [4. Documentação/Comentários](#4-documentaçãocomentários)
        - [4.1 Documentação](#41-documentação)
        - [4.2 Outras diretrizes para comentários](#42-outras-diretrizes-para-comentários)

## 1. Formatação de código

* **1.1** Use 4 espaços para tabs. Configure-os da seguinte forma:

<img width="749" alt="screen shot 2016-02-10 at 15 29 59" src="https://cloud.githubusercontent.com/assets/3029684/12940329/3566d882-d00b-11e5-9c2d-344f5c5f70e5.png" />

* **1.2** Ao acionar o comando ***control + i***, para indentar o código, não deve mudar nada.
* **1.3** A abertura de chaves deve seguir na mesma linha do método, função e etc. Além de conter um espaço antes. No caso do `else` do `if`, o mesmo deve acompanhar a linha de fechamento de chaves (` } `) do `if`.

```swift
// Certo
class UseClass {
    func useMethod() {
        if x == y {
            /* ... */
        } else if x == z {
            /* ... */
        } else {
            /* ... */
        }
    }

    /* ... */
}

// Errado
class UseClass
{
    func useMethod() 
    {
        if x == y 
        {
            /* ... */
        } 
        else if x == z 
        {
            /* ... */
        } 
        else 
        {
            /* ... */
        }
    }
    /* ... */
}
```

* **1.4** Todas as funções devem ser separadas uma da outra por uma linha vazia.

```swift
// Certo
class UseViewController: UIViewController {
    // ...

    override viewDidLoad() {
        // ...
    }

    override viewWillAppear(animated: Bool) {
        // ...
    }
}

// Errado
class UseViewController: UIViewController {
    // ...
    override viewDidLoad() {
        // ...
    }
    override viewWillAppear(animated: Bool) {
        // ...
    }
}
```

* **1.5** Ao escrever um tipo para constante, variável, propriedade e etc não adicionar espaço antes dos dois pontos (` : `) e adicionar um depois.

```swift
// Certo
func createItem(item: Item)

// Errado
func createItem(item:Item)
func createItem(item :Item)
```

* **1.6** A abertura de chaves (` { `) para declarações de tipos, funções e closures não devem ser acompanhadas de uma linha vazia. Declarações curtas de apenas uma linha podem ser escritas em seguida da abertura de chaves.

```swift
// Certo
class Icon {
    let image: UIImage
    init(image: UIImage) {
        self.image = image
        self.completion = { [weak self] in print("done"); self?.didComplete() }
    }

    func doSomething() { self.doSomethingElse() }
}

// Errado
class Icon {
    let image: UIImage
    var completion: (() -> Void)
    init(image: UIImage) {

        self.image = image
        self.completion = { [weak self] in self?.didComplete() }
    }

    func doSomething() {

        self.doSomethingElse()
    }
}
```

* **1.7** Declarações vazias devem ser escritas em chaves vazias (` {} `), sem que tenha quebra de linha entre elas.

```swift
// Certo
extension Icon: Equatable {}

// Errado
extension Icon: Equatable {
}
```

* **1.8** Ao usar vírgula (` , `) deve ser adicionado um espaço depois e não conter espaço algum antes.

```swift
// Certo
let array = [1, 2, 3]

// Errado
let array = [1,2,3]
let array = [1 ,2 ,3]
let array = [1 , 2 , 3]
```

* **1.9** Inserir um espaço antes e depois de operadores binários (` +, -, *, / e etc `), flecha de retorno (` -> `) e conter um espaço antes de abrir parenteses e um depois de fechar.

```swift
// Certo
let useConstant = 5 + (10 / 2) * 5 - 10

if 1 + 1 == 3 {
    fatalError("Isso não pode estar certo.")
}

func useReturn(value: Int) -> Int {
    /* ... */
}

// Errado
let useConstant = 5+(10/2)*5-10

if 1+1==3 {
    fatalError("Isso não pode estar certo.")
}

func useReturn(value: Int)->Int {
    /* ... */
}
```


* **1.10** Quando chamar uma função de múltiplos parâmetros, colocar cada parâmetro em uma linha.

```swift
// Certo
useFunction(firstValue: "Usemobile",
            secondValue: usemobileValue(),
            thirdValue: usemobileProperty)


// Errado
useFunction(firstValue: "Usemobile", secondValue: usmobileValue(), thirdValue: usemobileProperty)
```

* **1.11** Quando lidarmos com um array ou dicionário grande o suficiente para explicitar em múltiplas linhas, usar os colchetes (` [] `) como braços de um método.

```swift
// Certo
useFunctionWithManyArguments(randomStringArgument: "Esse é um argumento do tipo String",
                             randomArrayArgument: ["Esse é o primeiro argumeto de um array",
                                                   "Poderia esse ser o segundo argumento do array?"],
                             randomDictionaryArgument: ["primeiro valor do dictionary": "Posso ser o primeiro valor do dictionary?",
                                                        "segundo valor do dictionary": "Sim, claro que pode."],
                             randomClosure: { useParameter in
                                                print(useParameter)
                             })


// Errado
someFunctionWithABunchOfArguments(randomStringArgument: "Esse é um argumento do tipo String", randomArrayArgument: ["Esse é o primeiro argumeto de um array", "Poderia esse ser o segundo argumento do array?"] andomDictionaryArgument: ["primeiro valor do dictionary": "Posso ser o primeiro valor do dictionary?", "segundo valor do dictionary": "Sim, claro que pode."], randomClosure: { useParameter in print(useParameter)})
```

* **1.12** Usar constantes locais ou outras técnicas de mitigação para evitar múltiplas linhas.

```swift
// Certo
let firstCondition = x == firstReallyReallyLongPredicateFunction()
let secondCondition = y == secondReallyReallyLongPredicateFunction()
let thirdCondition = z == thirdReallyReallyLongPredicateFunction()
if firstCondition && secondCondition && thirdCondition {
    // do something
}

// Errado
if x == firstReallyReallyLongPredicateFunction()
    && y == secondReallyReallyLongPredicateFunction()
    && z == thirdReallyReallyLongPredicateFunction() {
        // do something
}
```

## 2. Nomenclatura

* **2.1** Usar UpperCamelCase para os tipos `struct`, `enum`, `class`, `typedef`, `associatedtype`, etc.
* **2.2** Usa camelCase para funções, métodos, propriedades, constantes, variáveis, argumentos, casos enum, etc. 
* **2.3** Quando lidarmos com acrônimos como HTML, URL, ID e etc manter letras maiúsculas exceto o caso do HTML que se usado para descrever variáveis e constantes deve ser em letras minúsculas.

```swift
// Certo
let htmlBodyContent: String = "<p>Somos a Usemobile!</p>"
let userID: Int = 12345
class URLSearch {
    /* ... */
}


// Errado
let HtmlBodyContent: String = "<p>Somos a Usemobile!</p>"
let userId: Int = 12345
class urlSearch {
    /* ... */
}
```

* **2.4** Nomes devem ser autodescritivos e nunca ambíguos. Além de padronizar a nomenclatura como o tipo do objeto antes do nome.

```swift
// Certo
class ButtonRoundAnimating: UIButton { /* ... */ }
@IBOutlet weak var lblSomething: UILabel!
@IBOutlet weak var txfSomething: Textfield!
@IBOutlet weak var swtSomething: UISwitch!
@IBOutlet weak var txvSomething: UITextView!
@IBOutlet weak var btnSomething: UIButton!

@IBAction func btnSomethingPressed(_ sender: Any) {

}

@IBAction func btnSomethingElsePressed(_ sender: UIButton!) {

}


// Errado
class ButtomCustom: UIButton { /* ... */ }
@IBOutlet weak var somethingLabel: UILabel!
@IBOutlet weak var somethingTextField: Textfield!
@IBOutlet weak var somethingSwitch: UISwitch!
@IBOutlet weak var somethingTextView: UITextView!
@IBOutlet weak var somethingButton: UIButton!

@IBAction func actionSomething(_ sender: Any) {

}

@IBAction func actionSomethingElse(_ sender: UIButton!) {

}
```

* **2.5** Nunca abreviar ou usar única letra para nomes. Usar nomes curtos.

```swift
// Certo
class RoundAnimatingButton: UIButton {

    let animationDuration: NSTimeInterval

    func startAnimating() {
        let firstSubview = subviews.first
    }

}

// Errado
class RoundAnimating: UIButton {
    let aniDur: NSTimeInterval
    func srtAnmating() {
        let v = subviews.first
    }
}
```


* **2.6**  Incluir tipo de objeto para nomes de constantes e variáveis quando não for óbvio. Quando criar uma `let` para uma `View Controller`, nomea-la como `somethingController` ocultando o `View`. E nunca usar `somethingView`, pois é uma `Controller` e não uma `View`.

```swift
// Certo
let personImageView: UIImageView
let animationDuration: TimeInterval
let number: Int = 15.0
let name: String = "Meu Nome"

// Errado
let text = UILabel()
let animation = TimeInterval(0.0)
let number = 15.0
let name = "Meu Nome"
```

* **2.7** Quando nomear funções, tenha certeza de que o nome seja autodescritivo.
* **2.8** Ao nomear o objeto, acrescente o sufixo `String` quando o objeto for do tipo `String`.

```swift
// Certo
var requestURL: NSURL
var sourceURLString: String
func loadURL(URL: NSURL) {
    // ...
}
func loadURLString(URLString: String) {
    // ...
}

// Errado
var requestURL: NSURL
var sourceURL: String
func loadURL(URL: NSURL) {
    // ...
}
func loadURL(URL: String) {
    // ...
}
```

* **2.9** Não referencie o construtor `class`, `struct`, `enum`, `protocol` e etc em seus nomes.

```swift
// Certo
class User {
    // ...
}
enum Result {
    // ...
}
protocol Queryable {
    // ...
}

// Errado
class UserClass {
    // ...
}
enum ResultEnum {
    // ...
}
protocol QueryableProtocol {
    // ...
}
```

## 3. Estilo de código

### 3.1 Geral

* **3.1.1** Use `let` ao invés de `var` sempre que possível.

* **3.1.2** Dê preferencia para composição de `map`, `filter`, `reduce`, etc. ao invés de interagir quando transformar de uma coleção para outra. Assegure-se de evitar usar `closures` que tem efeitos laterais quando usados em métodos.

```swift
// Certo
let stringOfInts = [1, 2, 3].flatMap { String($0) }
// ["1", "2", "3"]

// Errado
var stringOfInts: [String] = []
for integer in [1, 2, 3] {
    stringOfInts.append(String(integer))
}

// Certo
let evenNumbers = [4, 8, 15, 16, 23, 42].filter { $0 % 2 == 0 }
// [4, 8, 16, 42]

// Errado
var evenNumbers: [Int] = []
for integer in [4, 8, 15, 16, 23, 42] {
    if integer % 2 == 0 {
        evenNumbers.append(integer)
    }
}
```

* **3.1.3** Não declare o tipo para constantes e variáveis se elas podem inferir em seus nomes.

* **3.1.4** Se uma função retornar múltiplos valores, retorne uma tuple para usar argumentos `inout` (é melhor usar tuples em forma de label para clareza a não ser que seja óbvio). Se você usar uma certa tuple mais de uma vez, considere usar um `typealias`. Se você retornar 3 itens ou mais em uma tuple, consiedere usar um `struct`ou `class`.  

```swift
func myName() -> (firstName: String, lastName: String) {
    return ("Jose", "Silva")
}

let name = myName()
let firstName = name.firstName
let lastName = name.lastName
```


* **3.1.5** Não coloque parênteses envolvendo as condições de um if, guard etc.

```swift
// Certo
if x == y {
    /* ... */
}

// Errado
if (x == y) {
    /* ... */
}
```

* **3.1.6** Evite escrever um tipo `enum` quando possível - use o shorthand.

```swift
// Correto
imageView.setImageWithURL(url, type: .person)

// Errado
imageView.setImageWithURL(url, type: AsyncImageView.Type.person)
```

* **3.1.7** Não use shorthand para métodos de classe desde que geralmente é mais difícil inferir o contexto ao contrário do caso do `enum`.

```swift
// Correto
imageView.backgroundColor = UIColor.white

// Errado
imageView.backgroundColor = .white
```

* **3.1.7** Escreva `self.` sempre dentro de uma classe sempre que for acessar ou modificar um parâmetro próprio da classe.

* **3.1.8** Quando escrever um método, tenha em mente se pretende, alguma hora, sobrescrever o método ou não. Se não, marque-o como `final`, assim você previne que em algum momento lá na frente ele seja sobrescrito. Em geral, o método `final` é usado para diminuir o tempo de compilação, então é bom usar quando aplicável. Tome bastante cuidado, quando aplicar `final` em uma biblioteca, pois muitas vezes vai ser necessário customizar algo de sua biblioteca e usando `final` não será possível. 

* **3.1.9** Quando usar o statment `else`, `catch`, etc. que possui um bloco de execução, insira-o na mesma linha do bloco. Exemplos de `if`/`else` e `do`/`catch` abaixo.

```swift
if someBoolean {
    // do something
} else {
    // do something else
}

do {
    let fileContents = try readFile("filename.txt")
} catch {
    print(error)
}
```

* **3.1.10** Use `static` para uma classe declarando a função ou propriedade que é associada com a classe, ao contrário de uma instância daquela classe. Só use `class` se você especificamente precisa da funcionalidade de sobrescrever a função ou propriedade em um subclasse, logo considere usar um `protocol` para realizar essa atividade.

* **3.1.11** Se você tem uma função que não possui argumentos de entrada, não tem efeitos colaterais, e retorna algum objeto ou valor, use computed property.


### 3.2 Modificadores de acesso

* **3.2.1** Escreva o modifier keyword antes de todos os outros métodos, quando for utilizado.

```swift
// Correto
private static let myPrivateNumber: Int

// Errado
static private let myPrivateNumber: Int
```

* **3.2.2** O modifier keyword deve estar na mesma linha do que ele está descrevendo e não em linhas diferentes.

```swift
// Correto
open class Usemobile {
    /* ... */
}

// Errado
open
class Usemobile {
    /* ... */
}
```

* **3.2.3** Em geral, não escreva `internal` já que ele é padrão.

* **3.2.4** Use `private` ao invés de `fileprivate` quando possível.


### 3.3 Switch Statements and `enum`s

* **3.3.1** Quando usar `switch` que possui possibilidades finitas como é o caso do `enum`, não inclua o caso `default`. Ao invés, inclua os casos nao usados com um break em baixo.

* **3.3.2** Como os casos `switch`, por padrão já vem com o break, não o inclua a não ser que seja necessário.

* **3.3.3** Os `case` statements devem seguir alinhados com o `switch` statement como por padrão do Swift.

* **3.3.4** Quando definir um caso que é associado a um valor, assegure-se de que o valor é apropriadamente rotulado (utilize `case Hunger(hungerLevel: Int)` ao invés de `case Hunger(Int)`).

```swift
enum Problem {
    case attitude
    case hair
    case hunger(hungerLevel: Int)
}

func handleProblem(problem: Problem) {
    switch problem {
    case .attitude:
        print("Pelo menos eu não tenho um problema de cabelo.")
    case .hair:
        print("Seu cabeleleiro não soube a hora de parar.")
    case .hunger(let hungerLevel):
        print("O nível de fome é \(hungerLevel).")
    }
}
```

* **3.3.5** Use lista de possibilidades como em `case 1, 2, 3:` para usar o `fallthrough` keyword sempre que possível.

* **3.3.6** Se você tem um caso `default` que nao deveria ser alcançado, use um `throw` com um erro para lidar com a situação como segue abaixo.

```swift
func handleDigit(_ digit: Int) throws {
    switch digit {
    case 0, 1, 2, 3, 4, 5, 6, 7, 8, 9:
        print("Sim, \(digit) é um dígito!")
    default:
        throw Error(message: "O número fornecido não é um dígito.")
    }
}
```

### 3.4 Opcionais

* **3.4.1** A única vez que deve-se desembrulhar opcionais é com `@IBOutlets`. Em qualquer outro caso é melhor usar não-opcional ou opcional regular. Sim, tem casos em que você provavelmente garante que a propriedade nunca será `nil` quando usada, porem é melhor ser seguro e consistente. Similarmente não force desembrulhar.


* **3.4.2** Não use `as!` ou `try!` sempre que possível.

* **3.4.3** Se você não planeja usar o valor armazenado dentro de um opcional, mas precisa determinar quando é ou não `nil`, cheque se o valor de fato é `nil` ao invés de usar a sintaxe `if`.

```swift
// Correto
if someOptional != nil {
    // do something
}

// Errado
if let _ = someOptional {
    // do something
}
```

* **3.4.4** Não use `unowned`. Você pode pensar em `unowned` como equivalente da propriedade `weak` que é implicitamente desembrulhada. Como não queremos ocultar quando desembrulhamos algum objeto, não usamos `unowned`.

```swift
// Correto
weak var useViewController: UIViewController?

// Errado
weak var useViewController: UIViewController!
unowned var useViewController: UIViewController
```

* **3.4.5** Quando desembrullhar opcionais, use o mesmo nome para a constante ou variável desembrulhada quando apropriado.

```swift
guard let useValue = useValue else { return }
```


### 3.5 Protocols

Quando implementar `protocols`, há duas formas de organizar o código:

1. Usar o comentário `// MARK: -`  para separar a implementação de um protocolo do resto do código.
2. Usar um `extension` fora da classe ou `struct`, mas no mesmo source file.

Tenha em mente que usando uma `extension`, no entanto, o método na `extension` não pode sobrescrever sua subclasse, o que testar pode se tornar difícil.

Usa-se os 2, porém para o método #2 usar `extension` para delegates tipo UITableViewDelegate, UITextViewDelegate, UITableViewDataSource, etc.

### 3.6 Propriedades

* **3.6.1** Se fizer apenas leitura, computed propety, provém um getter sem método `get {}` o envolvendo.

```swift
var computedProperty: String {
    if someBool {
        return "Eu sou um desenvolvedor iOS na Usemobile!"
    }
    return "Estou desenvolvendo apps iOS."
}
```

* **3.6.2** Quando usar métodos `get {}`, `set {}`, `willSet` e `didSet` indentar esses blocos.
* **3.6.3** Apesar de você poder criar um nome personalizado para o valor antigo e novo para `willSet`/`didSet` e `set`, use os identificadores `newValue`/`oldValue` que são padrões.

```swift
var storedProperty: String = "Estou vendendo esse ótimo casaco." {
    willSet {
        print("o novo valor será \(newValue)")
    }
    didSet {
        print("o valor foi alterado de \(oldValue) para \(storedProperty)")
    }
}

var computedProperty: String  {
    get {
        if someBool {
            return "Sou um desenvolvedor iOS!"
        }
        return storedProperty
    }
    set {
        storedProperty = newValue
    }
}
```

* **3.6.4** Você pode declarar uma propriedade singleton como se segue:

```swift
class UsemobileManager {
    static let shared = appManager()

    /* ... */
}
```

### 3.7 Closures

* **3.7.1** Se o tipo dos parâmetros é óbvio, é tranquilo omitir o mesmo, mas explicitá-lo também é ok. Algumas vezes, a legibilidade é alcançada por estar detalhado e algumas vezes por não apresentar repetitividade.

```swift
// ocultando o tipo
doSomethingWithClosure() { response in
    print(response)
}

// explicitando type
doSomethingWithClosure() { response: NSURLResponse in
    print(response)
}

// usando shorthand no map statement
[1, 2, 3].flatMap { String($0) }
```

* **3.7.2** Quando usar closures, use parênteses `()` para indicar que não tem argumentos de entrada e `void` para indicar que retorna nada para esses casos.

```swift
let completionBlock: (Bool) -> Void = { (success) in
    print("Sucesso? \(success)")
}

let completionBlock: () -> Void = {
    print("Completedo!")
}

let completionBlock: (() -> Void)? = nil
```

* **3.7.3** Mantenha os nomes parâmetros na mesma linha de abertura de chaves (`{`) do closure.
* **3.7.4** Use a sintaxe de fechamento de closure a não ser que seja difícil compreender sem o parâmetro de nome. Exemplo a seguir:

```swift
// Certo
doSomething(1.0) { (parameter1) in
    print("Parameter 1 is \(parameter1)")
}

// Errado
doSomething(1.0, success: { (parameter1) in
    print("Sucesso com \(parameter1)")
}, failure: { (parameter1) in
    print("Falha com \(parameter1)")
})
```

### 3.8 Arrays

* **3.8.1** Em geral, use `.first` ou `.last` para acessar esses índices, sem usar subscripts. Use a sintaxe `for item in items`, quando possível, ao invés de `for i in 0..< items.count`. Você pode usar `for (index, value) in items.enumerated()` para acessar ambos, índice e valor.
* **3.9.2** Nunca use `+=` ou `+` para realizar append/concatenate em arrays. Use `.append()` ou `.append(contentsOf:)` por serem melhores quanto a compilação do projeto. Se deseja criar um novo array baseado na soma de dois arrays, use `let myNewArray = [arr1,arr2].flatten()` ao invés de `let myNewArray = arr1 + arr2`.

### 3.9 Lidando com erros

Suponhamos que uma função deve retornar uma `String`, só que em um certo momento cai em um erro. Uma forma opcional de resolver o problema, é colocar a função para retornar uma `String?` e retornar  `nil` para o caso de ocorrer erro.

Exemplo:

```swift
func readFile(named filename: String) -> String? {
    guard let file = openFile(named: filename) else {
        return nil
    }

    let fileContents = file.read()
    file.close()
    return fileContents
}

func printSomeFile() {
    let filename = "somefile.txt"
    guard let fileContents = readFile(named: filename) else {
        print("Não foi possível abrir o arquivo \(filename).")
        return
    }
    print(fileContents)
}
```

Invés disso, devemos usar o comportamento `try`/`catch` do Swift sabendo a razão da falha.

Você pode usar um `struct` como se segue:

```swift
struct Error: Swift.Error {
    public let file: StaticString
    public let function: StaticString
    public let line: UInt
    public let message: String

    public init(message: String, file: StaticString = #file, function: StaticString = #function, line: UInt = #line) {
        self.file = file
        self.function = function
        self.line = line
        self.message = message
    }
}
```

Mas a forma mais correta de se lidar com esse tipo de problema é como feito a seguir:

```swift
func readFile(named filename: String) throws -> String {
    guard let file = openFile(named: filename) else {
        throw Error(message: "Incapaz de abrir o arquivo \(filename).")
    }

    let fileContents = file.read()
    file.close()
    return fileContents
}

func printSomeFile() {
    do {
        let fileContents = try readFile(named: filename)
        print(fileContents)
    } catch {
        print(error)
    }
}
```

### 3.10 Usando `guard` Statements

* **3.10.1** Em geral, usamos um 'retorno mais cedo' ao invés de poluir o código com `if` statements. Usando `guard` statements para esses casos torna o código mais legível.

```swift
// Certo
func eatDoughnut(at index: Int) {
    guard index >= 0 && index < doughnuts.count else {
        // return early because the index is out of bounds
        return
    }

    let doughnut = doughnuts[index]
    eat(doughnut)
}

// Errado
func eatDoughnut(at index: Int) {
    if index >= 0 && index < doughnuts.count {
        let doughnut = doughnuts[index]
        eat(doughnut)
    }
}
```

* **3.10.2** Quando desembrulhar opcionais, use `guard` ao invés de `if` para diminuir o número de linha de código e aumentar a legibilidade.

```swift
// Certo
guard let monkeyIsland = monkeyIsland else {
    return
}
bookVacation(on: monkeyIsland)
bragAboutVacation(at: monkeyIsland)

// Errado
if let monkeyIsland = monkeyIsland {
    bookVacation(on: monkeyIsland)
    bragAboutVacation(at: monkeyIsland)
}

// Mais errado ainda
if monkeyIsland == nil {
    return
}
bookVacation(on: monkeyIsland!)
bragAboutVacation(at: monkeyIsland!)
```

* **3.10.3** Quando declarar um `if` ou `guard` para desembrulhar opcionais, o mais importante é manter a legibilidade do código. Existem diversas formas de se resolver isso envolvendo booleans e lógicas complexas. Quando estiver seguro de usar um `guard` ou `if` para desembrulhalos, use `guard`. Este é o padrão.

```swift
// um `if` legível
if operationFailed {
    return
}

// um `guard` legível
guard isSuccessful else {
    return
}

// a negação pode tornar e difícil a leitura do código.
guard !operationFailed else {
    return
}
```

* **3.10.4**  Se tiver de escolher dois estados diferentes, ai sim faz mais sentido usar `if` ao contrário de `guard`.

```swift
// Certo
if isFriendly {
    print("Olá, prazer em te conhecer!")
} else {
    print("Você é muito mal educado.")
}

// Errado
guard isFriendly else {
    print("Você é muito mal educado.")
    return
}

print("Olá, prazer em te conhecer!")
```

* **3.10.5** Você deve usar `guard` somente em caso de uma falha ocorrer e não houver problema do código continuar nas linha a baixo. Caso contrário, use o `if` como no exemplo descrito. 

```swift
if let monkeyIsland = monkeyIsland {
    bookVacation(onIsland: monkeyIsland)
}

if let woodchuck = woodchuck, canChuckWood(woodchuck) {
    woodchuck.chuckWood()
}
```

* **3.10.6** Frequentemente, caimos em situações que precisamos de desembrulhar vários opcionais usando `guard`. Em geral, desembrulhar vários opcionais em um único `guard` é mais rapido e simples de ser feito. Mas separando-os e retornando um erro específico é mais fácil de lidar com os problemas que surgirem.

```swift
// desembrulhar vários opcionais em um único `guard`
guard let thingOne = thingOne, let thingTwo = thingTwo, let thingThree = thingThree else { return }

//separá-los em diferentes `guard` retornando erro.
guard let thingOne = thingOne else { throw Error(message: "Falha ao desembrulhar thingOne.") }

guard let thingTwo = thingTwo else { throw Error(message: "Falha ao desembrulhar thingTwo.") }

guard let thingThree = thingThree else { throw Error(message: "Falha ao desembrulhar hingThree.") }
```

* **3.10.7** Use `guard` em uma única linha.


```swift
// Certo
guard let thingOne = thingOne else { return }

// Errado
guard let thingOne = thingOne else {
    return
}
```

### 3.11 Importando Bibliotecas

Declarações `import` para estruturas OS e estruturas externas devem ser separadas e organizdas alfabeticamente.

```swift
// Certo
import Foundation
import UIKit

import Alamofire
import Cartography
import SwiftyJSON

// Errado
import Cartography
import Foundation
import SwiftyJSON
import UIKit
import Alamofire
```

### 3.12 Proteção contra Dynamic

Todas implementações de Objective-C protocol, propriedades ou métodos, devem ser prefixados com `@objc dynamic`.

```swift
// Certo
@objc dynamic func scrollViewDidScroll(scrollView: UIScrollView) {
    // ...
}

// Errado
func scrollViewDidScroll(scrollView: UIScrollView) {
    // ...
}
```

### 3.13 TODO

Marque no código alterações que devem ser realizadas posteriormente com o `// TODO: - `.

Ao desenvolver um app que possui tela de login, por exemplo, durante a fase de testes você pode economizar tempo inicializando os parâmetros de login com valores pré determinados, porém ao terminar seu app você deve remover as linhas de código que fazem essa atribuição. Com o uso da marcação TODO, ao terminar seu app você lembrará de remover essas linhas indesejadas de código da versão final e saberá exatamente onde estão localizadas.

```swift
// MARK: - IBOutlets and IBActions

@IBOutlet weak var txfEmail: UITextfield!
@IBOutlet weak var txfPassword: UITextfield!

// MARK: - App Life Cycle

override func viewDidLoad() {
    super.viewDidLoad()
    

    // TODO: - Remove this credencials.

    self.txfEmail.text = "desenvolvedor@usemobile.xyz"
    self.txfPassword.text = "MinhaSenha"
}
```

### 3.14 Organização de Código

Os grupos para marcações (` // MARK: - `) devem ser ordenados da seguinte maneira:

* // MARK: - IBOutlets and IBActions
* // MARK: - Vars, lets and enums
* // MARK: - App Life Cycle (viewDidLoad, viewWillAppear e viewDidAppear)
* // MARK: - Local Functions
* Herança de protocolo (extensions):
    - // MARK: - UITableViewDataSource
    - // MARK: - UIScrollViewDelegate
    - // MARK: - UITableViewDelegate

```swift

class LoginViewController: UIViewController {


    // MARK: - IBOutlets and IBActions

    @IBOutlet weak var txfEmail: UITextfield!
    @IBOutlet weak var txfPassword: UITextfield!

    @IBAction func btnLoginPressed(_ sender: Any) {
        self.signIn(txfEmail.text, txfPassword.text)
    }


    // MARK: - Vars, lets and enums

    let userName : String = "desenvolvedor@usemobile.xyz"
    let userPassword : String = "MinhaSenha"

    // MARK: - App Life Cycle

    override func viewDidLoad() {
        super.viewDidLoad()


        // TODO: - Remove this credencials.

        self.txfEmail.text = userName
        self.txfPassword.text = userPassword
    }


    // MARK: - Local Functions

    func signIn (_ name: String, _ password: String){
        // Faz login do usuário
    }

}


// MARK: - UITextFieldDelegate

extension LoginViewController: UITextFieldDelegate {

    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        return true
    }

}
```


### 3.15 Boas Práticas

Em geral, nenhum aviso do Xcode deve ser ignorado.


## 4. Documentação/Comentários

### 4.1 Documentação

Para funções muito complexas, certifique-se de adicionar um comentário no seu topo descrevendo o que ela faz.

Diretriz:

* **4.1.1** Mesmo para comentários de uma linha, use `/** */`.

* **4.1.2** Nunca use prefixo adicional `*` a cada linha

* **4.1.3** Use a sintaxe `- parameter` ao invés do antigo `:param:`.

```swift
class Human {
    /**
     This method feeds a certain food to a person.

     - parameter food: The food you want to be eaten.
     - parameter person: The person who should eat the food.
     - returns: True if the food was eaten by the person; false otherwise.
    */
    func feed(_ food: Food, to person: Human) -> Bool {
        // ...
    }
}
```

* **4.1.4** Para classes complicadas, descreva-as, como usa-las e com exemplos.

```swift
/**
 ## Feature Support

 This class does some awesome things. It supports:

 - Feature 1
 - Feature 2
 - Feature 3

 ## Examples

 Here is an example use case indented by four spaces because that indicates a
 code block:

     let myAwesomeThing = MyAwesomeClass()
     myAwesomeThing.makeMoney()

 ## Warnings

 There are some things you should be careful of:

 1. Thing one
 2. Thing two
 3. Thing three
 */
class MyAwesomeClass {
    /* ... */
}
```

* **4.1.7** Quando mencionar algo do código, envolva-os com aspas ` '' `

```swift
/**
 This does something with a `UIViewController`, perchance.
 - warning: Make sure that `someValue` is `true` before running this function.
 */
func myFunction() {
    /* ... */
}
```

### 4.2 Outras diretrizes para comentários

* **4.2.1** Sempre adicione um espaço depois do //
* **4.2.2** Quando usar `// Mark: - whatever`, deixe uma linha em branco a baixo e duas linhas em branco acima.


```swift
class Developer {


    // MARK: - instance properties

    private let developerName: String


    // MARK: - initialization

    init() {
        /* ... */
    }

}
```
