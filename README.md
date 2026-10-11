# Sistema Escolar — Spring Boot

Projeto base da atividade **Caça aos Erros** (Programação Web 1 · Senac Rio).

API REST de um sistema escolar de cadastro com **Professor**, **Aluno** e **Matrícula**,
usando Java 17, Spring Boot, Spring Data JPA e banco H2 em memória.

## Como executar

```bash
./mvnw spring-boot:run
```

Com o servidor rodando, teste os endpoints no Insomnia ou no Postman
(`/professores`, `/alunos` e `/matriculas`) e acesse o console do banco em
`http://localhost:8080/h2-console`.
