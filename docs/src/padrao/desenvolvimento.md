## __Pré requisitos__
O processo aqui documentado assume o seguinte contexto:

!!! tip ""
    - [x] &nbsp; Existe um projeto já inicializado e construído em algum repositório GitLab
    - [x] &nbsp; Python e Pip já estejam instalado na máquina
    - [x] &nbsp; O MKDocs e suas dependências já estejam configurados no `requirements.txt` 
    - [x] &nbsp; A funcionalidade **GitLab pages** já esteja configurada
    - [x] &nbsp; Já existe uma documentação para fazer o deploy

## __Objetivo__
O [MKDocs](https://www.mkdocs.org/) é um gerador de páginas estáticas para criação de documentação modernas e que podem ser hospedadas no gitlab pages. O objetivo deste documento é apresentar um possível padrão para as documentações de desenvolvimento de uma aplicação.

O processo de deploy aqui documentado irá passar pelos seguintes passos

!!! tip ""
    - [x] &nbsp; Como criar um novo documento
    - [x] &nbsp; Guias de ajuda onde você pode deixar os registros aprendidos no desenvolvimento

## __Criando um novo documento__

Com base na [arquitetura da documentação](./arquitetura.md), o primeiro passo é criar uma pasta com o nome da sua documentação em `assets` e `src`. Você usará essas duas pastas para armazenar os componentes visuais e os códigos respectivamente.

Após adicionar os arquivos de documentação `.md`, você precisará aponta-los no arquivo `mkdocs.yml` gerando a estrutura de navegação. No final desse arquivo há a tag `nav`, esse é o lugar onde você referenciará os seus arquivos de documentação.

```yml
nav:
    - Engenharia: 
      - src/engenharia/index.md
      - Começando: src/engenharia/getting_started.md
      - Arquitetura: src/engenharia/arquitetura/arquitetura.md
      - Deploy: src/engenharia/arquitetura/deploy.md
      - Ajuda: 
        - src/engenharia/ajuda/index.md
        - src/engenharia/ajuda/erro_no_deploy.md
```

Com isso escreva a sua documentação utilizando as tags do markdown ou do [MKDocs-material](https://squidfunk.github.io/mkdocs-material/). Acompanhe no Browser se as modificações estão sendo realizadas de forma coerente. Após isso, commit as modificações e suba para o GitLab. 

## __Ajuda__

!!! warning ""
    === "Tabelas"
        ```md
        {{read_table("padrao/projetos.csv", sep=',') }}
        ```

        {{ read_table("padrao/projetos.csv", sep=',') }}

    === "Imagem"
        ```md
        ![imagem da arquitetura](../../assets/padrao/arquitetura/arquitetura.png)
        ```

        ![imagem da arquitetura](../../assets/padrao/arquitetura/arquitetura.png)

    === "Texto"
        ```md
        ## __Título__
        **Negrito**
        *Itálico*
        `Destaque`
        ```
        
        ## __Título__

        **Negrito**

        *Itálico*

        `Destaque`
    
    === "Código"
        ```md
            ```bash
                export MODEL=model1 # (1)
            ```
            
            1. Variável com o nome do modelo 
        ```
        
        ```bash
            export MODEL=model1 # (1)
        ```

        1. Variável com o nome do modelo
    
        