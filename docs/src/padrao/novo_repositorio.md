# Novo repositório

## __Pré requisitos__
O processo aqui documentado assume o seguinte contexto:

!!! tip ""
    - [x] &nbsp; Existe um repositório no GitLab para documentação
    - [x] &nbsp; Já existe uma documentação para fazer o deploy
    - [x] &nbsp; Python e Pip já estejam instalado na máquina

## __Objetivo__
O [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/) é uma funcionalidade que possibilita publicar um website estático de um repositório GitLab. A ideia é que a documentação seja hospedada no GitLab Pages e versionada no repositório do projeto. Além disso, todo o deploy seja feito de forma automática utilizando o CI/CD.

O processo de deploy aqui documentado irá passar pelos seguintes passos

!!! tip ""
    - [x] &nbsp; Como instalar dependências necessárias para o MKDocs
    - [x] &nbsp; Iniciando com o MKDocs
    - [x] &nbsp; CI/CD
    - [x] &nbsp; Como configurar o repositório
    
## __Getting Started__

Nesse projeto estamos utilizando o [pip](https://pypi.org/project/pip/) como instalador de pacotes para o python. É recomendado utilizar um gerenciador de pacote como o [Poetry](https://python-poetry.org/docs/master/#installing-with-the-official-installer) ou o [Conda](https://docs.conda.io/en/latest/) para a criação de um ambiente virtual, porém **não é obrigatório**.

Para criar a documentação você precisará seguir a [documentação de instalação do MKDocs](https://www.mkdocs.org/user-guide/installation/) e do [MKDocs Material](https://squidfunk.github.io/mkdocs-material/getting-started/). Essas duas dependências são a base para a construção da documentação, porém outros plugins ou extensões pode ser adicionadas. Para gerar o `requirements.txt`, você pode dá o comando `pip freeze > requirements.txt`. 

Abaixo há um exemplo desse aquivo, onde você pode utiliza-lo e não se preocupar com as instalações de dependências. Para isso, crie um arquivo `requirements.txt`, cole nesse arquivos as dependências e execute o comando `pip3 install -r requirements.txt`.

```md title="requirements.txt"

click==8.1.3
ghp-import==2.1.0
importlib-metadata==4.12.0
Jinja2==3.1.2
Markdown==3.3.7
MarkupSafe==2.1.1
mergedeep==1.3.4
mkdocs==1.3.1
mkdocs-material==8.3.9
mkdocs-material-extensions==1.0.3
mkdocs-table-reader-plugin==1.1.0
numpy==1.23.2
packaging==21.3
pandas==1.4.3
Pygments==2.12.0
pymdown-extensions==9.5
pyparsing==3.0.9
python-dateutil==2.8.2
pytz==2022.2.1
PyYAML==6.0
pyyaml_env_tag==0.1
six==1.16.0
tabulate==0.8.10
watchdog==2.1.9
zipp==3.8.1

```

## __Iniciando o MKDocs__

Após instalar as dependências, você pode iniciar o mkdocs com :

```bash
mkdocs new docs
```

Em [Desenvolvimento](./desenvolvimento.md) você pode aprender como criar um novo documento.

Além disso, nossa documentação utiliza o tema da [mkdocs-material](https://github.com/squidfunk/mkdocs-material). Temas externos ficam na pasta **docs/material/overrides** e são apontados no arquivo `mkdocs.yml` da seguinte forma:

```yml
theme: 
  name: material
  custom_dir: !ENV [THEME_DIR, "material"]
```

## __CI/CD__

O CI/CD é configurado na arquivo `.gitlab-ci.yml`, é nesse arquivo que iremos adicionar o pipeline para o deploy automático de nossa documentação a cada novo commit.

```yml title=".gitlab-ci.yml"
image: python:3.8
before_script: 
    - pip install -r requirements.txt 

pages: 
  stage: build
  script:
    - mkdocs build
    - mv site public
  artifacts:
    paths: 
      - public
  only:
      - main

```

Após fazer o commit e o push, você pode acompanhar o pipeline dentro do repositório do projeto no GitLab em **CI/CD > Pipelines**. 

## __Configurando o repositório__

Dentro do repositório do projeto vá até a aba **Settings > Pages**. Nessa página você tem acesso ao link onde sua página está hospedada.

Em baixo de **Settings** tem a aba **General**, onde você pode configurar a visibilidade do seu site em **Visibility, project features, permissions > Pages**

## __Ajuda__

!!! warning ""
    === "Video do processo"
        - [Video de referência do processo aqui descrito](https://youtu.be/k7rkjVfuB2M)