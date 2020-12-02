# CWISEC - GitHub Code Scanning

Realizei uma POC para testar a nova funcionalidade do GitHub de Code Scanning, o qual analizva o código fonte e alertava sobre possíveis falhas e erros no código.

Nos meus testes consegui ver a ferramenta em funcionamento, mas ela não processou conforme esperado. No fim, não foi possível validar se ela seria util para um projeto real.

## 12/11 : Estudando sobre o Github Code Scanning

Comecei estudando sobre Code Scanning. Encontrei alguns videos e uma documentação do GitHub.

O Github Code Scanning utiliza a própria ferramenta de pipelines, o **Github Actions**, para rodar os asserts de código.

Neste caso, se o projeto for de código fechado, além de ter uma conta que possa utilizar o Code Scanning, deverá ter acesso aos Actions, que também é pago para projetos privados.

Então peguei um projeto Java que eu tinha, o qual nem validei se possuia mesmo falhas, para ver na prática como funcionava. Consegui colocar para rodar, mas não pegou nenhuma falha.

**Video / Documentações**

- [(GitHub Doc) Code Scanning](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code)

- [(GitHub Doc) Actions](https://docs.github.com/en/free-pro-team@latest/actions)

- [(YouTube) GitHub Actions & Code Scanning](https://www.youtube.com/watch?v=zgNFQY820Os)

## 16/11 : Testando a ferramenta

Dei uma lida na documentação do Github, vendo se possuia configurações para que funcione corretamente. A principio o arquivo padrão criado, com poucas mexidas em branch e linguagem bastaria para pegar falhas gerais.

Resolvi fazer um teste com um código em Javascript, uma api em NodeJS, que sabia que tinha algumas falhas.

Na primeira configuração não pegou nenhuma falha. Fiz mais alguns testes alterando o arquivo de configuração, mas não funcionou.

Como era um código pessoal, removi coisas sensiveis, fiz os testes e apaguei o projeto em seguida.

Fiz um fork de um projeto criado com propósito de expor falhas de segurança, apenas com a configuração basica também do Code Scanning. Neste pegou 44 falhas.

Aqui vi que apenas algumas linguagens funcionava, como **C++, C#, Java, Python e Javascript.**

Fork testado: https://github.com/jasperes/juice-shop

## 17/11 : Novos testes específicos em Python

Continuei investigando a documentação do Github para ver se tinha esquecido algo ou se tinha alguma configuração necessária para o funcionamento.

Algo importante que vi é que é possivel integrar outras plataformas de **Integração Continua**, como o **Jenkins**, com o Github Code Scanning. Este é um cenário quando cliente não consegue utilizar o **Actions** ou possui outra plataforma que não o GitHub.

Para testar novamente, fiz um código em Python com uma falha explicita de **SQL Injection**.

Novamente, na primeira tentativa não pegou nenhuma falha. Fiz então algumas alterações, conforme a documentação.

Alterei a forma de build, forcei a utilização de validação das dependencias do arquivo requirements.txt, forcei alguns cenários de teste.

Por fim, consegui exibir a falha de segurança na **aba Security**.

Porém, o pipeline da Action deu sucesso e em Pull Request também não criticou falha. Deixei para fazer estes testes em outro momento.

Repo testado: https://github.com/jasperes/teste123

## 23/11 : Criando projeto com varias falhas

Criei um repositório novo com varias falhas de segurança, em Python. São elas: **SQL Injection, Chaves Abertas, HTML Injection, Code Injection, OS Command Injection.**

Como de costume, comecei os testes com o arquivo de configuração padrão. Não pegou nenhuma falha.

Validei no console da Action e vi que ele encontrou os scripts em Python. Então peguei exatamente o script que testei no outro repositório em Python e coloquei para rodar, não funcionou.

Nisto entrei na tentativa e erro. Testei colocar arquivos no root e mandar rodar, também não funcionou.

Neste pegou apenas falha de importação não utilizada. Fiz a correção e ele colocou o alerta para "resolvidos".

Por fim, criei um novo repositório, pegando todo o código quebrado de varios testes e joguei em apenas um arquivo, tudo na raiz do projeto.

Fiz vários testes, començando pelo basico e fazendo alterações.

**Projetos criados**

- Principal: https://github.com/jasperes/poc-github-code-scanning
- Teste com tudo em um arquivo: https://github.com/jasperes/test456

## 24/11 - 25/11 : Tentativa e falha

Nos dois dias seguintes foram tentativa e erro. Vasculhei a documentação para ver se encontrava mais opções. Fiz varios testes de criar novos arquivos, fazer Pull Requests, alterar configuração.

Em nenhum caso pegou as falhas de segurança criadas. Ainda existem mais testes que podem ser feito, como em outra linguagem, uma estrutura real, etc.

O Github Code Scanning é uma ferramenta muito nova. Não encontrei nada util fora da documentação oficial, nem repositórios exemplos (que deixaram os alertas de falha aberto para visualizar).
