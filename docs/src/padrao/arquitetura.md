## __Objetivo__

O objetivo do documento é exibir a arquitetura utilizada no desenvolvimento da documentação utilizando o gerador de páginas estático [MKDocs](https://www.mkdocs.org/).

## __Organização__

Existe duas propostas de padrões utilizados nesse projeto: 

<center>

| **Ambiente** | **Descrição** |
|:-:|:-:|
| Desenvolvimento | Padrão para documentar o desenvolvimento da aplicação, onde há a descrição das funcionalidades e implementações de comandos e códigos |
| Arquitetura | Descrever a arquitetura ou a funcionalidade de forma mais conceitual, sem muitos detalhes de implementação |

</center>

## __Arquitetura do Projeto__

Suponha que você esteja documentando a `📂arquitetura_e_modelagem` dos dados do `📂projeto1`. Esse projeto possui uma imagem `📷arquitetura_gcp.png`, uma tabela `📋tabela.csv` e um documento chamado `📜arquitetura.md`. 

Com isso em mente, teremos a seguinte estrutura:

```bash hl_lines="3 4 7 8 11 12"
📦REPOSITÓRIO
┣ 📂docs
┃ ┣ 📂assets
┃ ┃ ┣ 📂projeto1
┃ ┃ ┃ ┣ 📂arquitetura_e_modelagem
┃ ┃ ┃ ┃ ┗ 📷arquitetura_gcp.png 
┃ ┃ ┣ 📂tables
┃ ┃ ┃ ┣ 📂projeto1
┃ ┃ ┃ ┃ ┣ 📂arquitetura_e_modelagem
┃ ┃ ┃ ┃ ┃ ┗ 📋tabela.csv 
┃ ┣ 📂src
┃ ┃ ┣ 📂projeto1
┃ ┃ ┃ ┣ 📂ajuda
┃ ┃ ┃ ┃ ┗ 📜index.md
┃ ┃ ┃ ┣ 📂arquitetura_e_modelagem
┃ ┃ ┃ ┃ ┗ 📜arquitetura.md
┣ 📜mkdocs.yml # (1)
┣ 📜.gitlab-ci.yml 
┗ 📜requirements.txt 
```

1. Configura as extensões e pluggins do MKDocs, além de permitir definir a navegação do site `nav`.

Perceba que uma pasta com o nome da documentação está armazenada em `assets`, `table` e `src`. É nessas pastas que você armazenará os arquivos visuais, tabelas e os arquivos markdown respectivamente. 

Caso a arquitetura precise ser fragmentada em módulos, você pode dividir no [`nav`](./desenvolvimento.md#criando-um-novo-documento) como apresentado abaixo.  A partir do segundo módulo os arquivos precisam ter apenas o objetivo e não precisam conter todos os tópicos aqui apresentados.


```yml
nav:
    - Alguma funcionalidade 1: 
      - index.md
      - Arquitetura: 
        - arquitetura.md
        - Modulo1: modulo1.md
        - Modulo2: modulo2.md
        - Modulo3: modulo3.md
```
