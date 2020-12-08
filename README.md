# Serializa��o

## Conceito

A serializa��o � quando um objeto � transformado, em uma cadeia de bytes e desta forma pode ser manipulado de maneira mais f�cil, seja atrav�s de transporte pela rede ou salvo no disco.

## Implementa��o

Para um objeto estar credenciado a passar pelo processo de serializa��o sua classe deve implementar a interface java.io.Serializable que sinalizar� a m�quina virtual Java (JVM) que objetos daquela classe est�o aptos a serem serializadas.

## Atributos n�o serializ�veis

Caso n�o se deseje serializar algum atributo de inst�ncia espec�fico de um determinado objeto, basta sinaliz�-lo como transient, assim o objeto serializado n�o conter� a informa��o referente a este atributo.

```java
private transient String password;
```

## Identifica��o

Toda classe serializada possui um serialVersionUID que identifica a vers�o da classe gerado pelo Java no momento da compila��o.

- Na deserializa��o, o construtor da classe n�o � chamado.

## For�ando serializa��o em uma classe

Caso voc� esteja utilizando uma classe que voc� n�o pode aplicar a serializa��o direta, implementando a interface, voc� poder� criar dois m�todos que far�o este processo mesmo que a classe que voc� queria usar n�o seja serializada.

Exemplo, temos a classe aluno que tem um atributo do tipo Turma mas por algum motivo voc� n�o pode implementar a serializa��o na Turma pois ela n�o te pertence, ent�o ficaria assim:

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