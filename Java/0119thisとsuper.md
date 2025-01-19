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
