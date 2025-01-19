# thisとsuper

|特徴	|this|super|
|:-----------------|:------------------|:-------------------|
|対象	|現在のクラスのインスタンスを参照	|親クラスのメンバーを参照|
|使える場所	|インスタンスメソッドやコンストラクタの中のみ	|子クラスのメソッドやコンストラクタの中のみ|
|主な用途|	同じクラスのメンバーやコンストラクタを呼び出す|	親クラスのメンバーやコンストラクタを呼び出す|
|呼び出し対象|	メソッド、変数、別のコンストラクタ|	メソッド、変数、親クラスのコンストラクタ|

## 使用用途
メソッド内で、引数やローカル変数がインスタンス変数と同じ名前の場合、thisを使ってインスタンス変数を明確に指定
```
public class Person {
    private String name;

    public void setName(String name) {
        // ローカル変数nameとインスタンス変数nameを区別
        this.name = name;
    }

    public void display() {
        System.out.println("Name: " + this.name);
    }
}

```


コンストラクタの呼び出し
this(引数)を使うと、別のコンストラクタを呼び出してコードの重複を避けることが可能
```
public class Person {
    private String name;
    private int age;

    // コンストラクタ1
    public Person(String name) {
        this(name, 0); // コンストラクタ2を呼び出し
    }

    // コンストラクタ2
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

```

## superの使い方
superは、親クラス（スーパークラス）のメンバーを参照するキーワード
親クラスのメソッドや変数を参照する。
親クラスのコンストラクタを呼び出す。

親クラスのメソッドや変数を参照

```
//親クラス
public class Person {
    public void display() {
        System.out.println("This is a Person.");
    }
}
```
```
// 子クラス
public class Student extends Person {
    @Override
    public void display() {
        super.display(); // 親クラスのdisplayメソッドを呼び出し
        System.out.println("This is a Student.");
    }
}
```

```
//　実行クラス
public class Main {
    public static void main(String[] args) {
        Student student = new Student();
        student.display();
    }
}
->This is a Person.
->This is a Student.
```

親クラスのコンストラクタを呼び出す
```
public class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }

    public void display() {
        System.out.println("Name: " + name);
    }
}
```

```
public class Student extends Person {
    private int studentId;

    public Student(String name, int studentId) {
        super(name); // 親クラスのコンストラクタを呼び出し
        this.studentId = studentId;
    }

    @Override
    public void display() {
        super.display(); // 親クラスのdisplayメソッドを呼び出し
        System.out.println("Student ID: " + studentId);
    }
}
```

```
public class Main {
    public static void main(String[] args) {
        Student student = new Student("Sato", 101);
        student.display();
    }
}
->Name: Sato
->Student ID: 101

```
子クラスのコンストラクタでは、必ず最初にsuper(...)を使って親クラスのコンストラクタを呼び出し

親クラスの初期化処理を正しく行うために必要

---

# 変数のthisと、メソッドのthis()の違い
|項目	|変数のthis	|メソッドのthis() |
|:-----------------|:------------------|:-------------------|
|目的|現在のインスタンスの変数やメソッドを参照する.ローカル変数や引数とインスタンス変数を区別するために使う|	現在のクラスの別のコンストラクタを呼び出す.コンストラクタのコードを再利用し、冗長な記述を避けるために使う|
|使用場所	|メソッドやコンストラクタ内	|コンストラクタの先頭のみ|
|対象	|インスタンス変数やインスタンスメソッド	|別のコンストラクタ|
|省略可能か|	名前の重複がなければ省略可能|	省略不可|
|動作のタイミング	|実行時	|コンストラクタ呼び出し時|

## 変数のthis
```
public class Person {
    private String name; // インスタンス変数

    public void setName(String name) { // 引数nameが存在
        this.name = name; // インスタンス変数nameに引数nameを代入
    }

    public void display() {
        System.out.println("Name: " + this.name);
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("Taro"); // 引数で"名前"を設定
        person.display();       // Name: Taro
    }
}

```
実行の流れ
setNameメソッドに引数nameが渡される。
this.nameはインスタンス変数を指し、単なるnameはローカル変数または引数を指す。
this.name = name; によって、引数nameの値がインスタンス変数nameに代入される。


## メソッドのthis()
コンストラクタの先頭でのみ使用可能。
引数のパターンによって、どのコンストラクタを呼び出すかが決定される。
```
public class Person {
    private String name;
    private int age;

    // コンストラクタ1: 名前のみを設定
    public Person(String name) {
        this(name, 0); // コンストラクタ2を呼び出し
    }

    // コンストラクタ2: 名前と年齢を設定
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void display() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Person person1 = new Person("Taro");         // コンストラクタ1を呼び出し
        Person person2 = new Person("Hanako", 25);   // コンストラクタ2を呼び出し

        person1.display(); // Name: Taro, Age: 0
        person2.display(); // Name: Hanako, Age: 25
    }
}

```
