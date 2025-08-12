# Projeto Admin Demo (JPA + Hibernate + SQLite)

Projeto Maven para cadastros de **Clientes (Pessoa)** e **Produtos** usando **JPA/Hibernate** com banco **SQLite**.

## 📦 Estrutura

jpa_hibernate/
├── pom.xml
├── database_admin.db # gerado em runtime
├── sql_schema_database_admin.sql # cole o schema exportado aqui
└── src/
└── main/
├── java/
│ ├── demo/ # AdministrativoApp (main)
│ ├── entities/ # @Entity: Pessoa, Produto
│ └── models/ # CRUD: PessoaModel, ProdutoModel
└── resources/
└── META-INF/
└── persistence.xml # config JPA/Hibernate/SQLite

markdown
Copiar
Editar

## 🔧 Configuração

- **GroupId**: `com.techcamps.cadastros`
- **ArtifactId**: `administrativo-api`
- **Java**: `1.8` (ajuste em `<maven.compiler.source/target>`)
- **Dependências**:
  - `hibernate-core:5.4.12.Final`
  - `hibernate-entitymanager:5.4.12.Final`
  - `sqlite-jdbc:3.36.0.3`
  - `sqlite-dialect:0.1.2`

**`persistence.xml`** (resumo):
- URL: `jdbc:sqlite:database_admin.db`
- Driver: `org.sqlite.JDBC`
- Dialect: `org.sqlite.hibernate.dialect.SQLiteDialect`
- `hibernate.hbm2ddl.auto=update`
- `show_sql=true`, `format_sql=true`

## ▶️ Executando

Na raiz do repositório:

```bash
# compilar
mvn -q -f jpa_hibernate/pom.xml clean compile

# executar a classe principal
# (se o exec-maven-plugin estiver configurado com mainClass)
mvn -q -f jpa_hibernate/pom.xml exec:java

# alternativa: indicar a main diretamente
mvn -q -f jpa_hibernate/pom.xml exec:java -Dexec.mainClass=demo.AdministrativoApp
A primeira execução cria/atualiza database_admin.db e as tabelas pessoas e produtos.

🗃️ Operações CRUD (onde procurar)
models/ProdutoModel.java: create, findById, findAll, update, delete

models/PessoaModel.java: create, findById, findAll, update, delete

demo/AdministrativoApp.java: exemplos de uso dos Models

🧪 Dica: exportar o Schema do SQLite
Abra database_admin.db no SQLite Online e exporte o SQL Schema de cada tabela, colando o resultado em:
jpa_hibernate/sql_schema_database_admin.sql.

⚠️ Observações
Date em JPA com @Temporal(TemporalType.DATE) persiste como TEXT ISO-8601 no SQLite.

Para resets completos, troque temporariamente hibernate.hbm2ddl.auto para create-drop (somente em dev).
