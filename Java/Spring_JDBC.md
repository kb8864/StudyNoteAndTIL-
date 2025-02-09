# Spring_JDBC
→Spring Framework が提供する JDBC（Java Database Connectivity） を簡単に扱うためのライブラリのこと
今回使うのはNamedParameterJdbcTemplate
NamedParameterJdbcTemplate は、SQLに名前付きパラメータを使えるようにした JdbcTemplate の拡張版。
通常の JdbcTemplate では ? を使ってパラメータを指定するが、
NamedParameterJdbcTemplate では :paramName のように 名前付きパラメータ を利用できる。

- メイン機能はJdbcTemplate を使ってSQLを簡潔に実行できる
- 
Spring JDBCのメリット<br>
✅ コードの簡素化	JdbcTemplate により、JDBCの定型コードを省略できる<br>
✅ リソース管理が不要	Connection や Statement のクローズを自動管理<br>
✅ 例外処理の統一	DataAccessException により、JDBCの SQLException をラップ<br>
✅ SQLを直接書ける	ORM（Hibernate など）と違い、シンプルにSQLを記述可能<br>

NamedParameterJdbcTemplateのメリット<br>
✅ 可読性が向上	? の代わりに :paramName を使うため、SQLの意味が分かりやすい<br>
✅ 順番を気にしなくてよい	? だと順番を間違えるとバグになるが、名前付きなら問題なし<br>
✅ パラメータの再利用がしやすい	MapSqlParameterSource を使ってパラメータを管理できる<br>


[学習教材](https://www.docswell.com/s/MasatoshiTada/5Q4EMZ-spring-101#p23)

