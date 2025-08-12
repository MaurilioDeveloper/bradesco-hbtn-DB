# Projeto Admin Demo

Maven + JPA/Hibernate + SQLite.

## Como executar
```bash
mvn -q -f jpa_hibernate/pom.xml clean compile
mvn -q -f jpa_hibernate/pom.xml exec:java -Dexec.mainClass=demo.AdministrativoApp
