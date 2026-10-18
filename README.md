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

# Erros encontrados:
1.no pom.xml o scope tava como test, troquei para runtime e o servidor passou a funcionar

2.no pom.xml só tinha uma das dependencias do h2, estava faltando a do h2-console, adicionei e consegui entrar 

3.em aluno.java this.ra = dados.curso();, corrigido para this.ra = dados.ra();

4.em matricula.java o private Aluno aluno recebia a anotação OneToOne que contradiz o comportamento esperado:
Um mesmo aluno pode ter várias matrículas
troquei por @ManyToOne permitindo o mesmo aluno ter varias matriculas

5.deu 500 no post do aluno dizendo que não tinha tabela criada no banco de dados ai tirei as 2 linhas a mais que tem no application-test.properties pra deixar igual o do vollmed (só trocando o nome de vollmeddb pra clinicadb) e funcionou criou as tabelas no h2

6.ao testar o put do aluno deu 200 mas nao trocou o curso para engenharia de software, verifiquei o AlunoController e estava faltando o @Transactional no metodo atualizar

7.ao testar o post do professor deu 500 e verifiquei o model professor.java e estava faltando @GeneratedValue(strategy = GenerationType.IDENTITY) no id do professor 

8.ao testar o post de matricula deu 500 e percebi que em matricula controller.java tinha 
Aluno aluno = alunoRepository.getReferenceById(dados.idAluno());
e no DTO DadosCadastroMatricula.java  tbm tinha idAluno mas no Json ele recebia alunoId, troquei idAluno por alunoId em ambos e funcionou

