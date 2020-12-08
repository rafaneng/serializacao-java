# Serialização

## Conceito

A serialização é quando um objeto é transformado, em uma cadeia de bytes e desta forma pode ser manipulado de maneira mais fácil, seja através de transporte pela rede ou salvo no disco.

## Implementação

Para um objeto estar credenciado a passar pelo processo de serialização sua classe deve implementar a interface java.io.Serializable que sinalizará a máquina virtual Java (JVM) que objetos daquela classe estão aptos a serem serializadas.

```java
public class Aluno implements Serializable
```

## Atributos não serializáveis

Caso não se deseje serializar algum atributo de instância específico de um determinado objeto, basta sinalizá-lo como transient, assim o objeto serializado não conterá a informação referente a este atributo.

```java
private transient String password;
```

## Identificação

Toda classe serializada possui um serialVersionUID que identifica a versão da classe gerado pelo Java no momento da compilação.

- Na deserialização, o construtor da classe não é chamado.

## Forçando serialização em uma classe

Caso você esteja utilizando uma classe que você não pode aplicar a serialização direta, implementando a interface, você poderá criar dois métodos que farão este processo mesmo que a classe que você queria usar não seja serializada.

Exemplo, temos a classe Aluno que tem um atributo do tipo Turma mas por algum motivo você não pode implementar a serialização na Turma pois ela não te pertence.
Então você implementaria estes dois métodos na classe Aluno:

```java
private void writeObject(ObjectOutputStream oos){
        try{
            oos.defaultWriteObject();
            oos.writeUTF(turma.getNome());
        }catch (IOException e){
            e.printStackTrace();
        }
    }

    private void readObject(ObjectInputStream ois){
        try{
            ois.defaultReadObject();
            turma = new Turma(ois.readUTF());
        }catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
```

## Referencias

[https://www.oracle.com/br/technical-resources/articles/java/serialversionuid.html](https://www.oracle.com/br/technical-resources/articles/java/serialversionuid.html)

[https://www.youtube.com/watch?v=5Rq6n-q471Q](https://www.youtube.com/watch?v=5Rq6n-q471Q)
