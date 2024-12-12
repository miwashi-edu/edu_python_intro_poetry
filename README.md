# edu_python_intro_poetry

[Poetry](https://python-poetry.org)
[toml](https://toml.io/en/)  
[masonry](https://python-poetry.org/docs/pyproject/#poetry-and-pep-517)

## instructions

> Requires yq is installed

```bash
cd ~
cd ws
mkdir my_python_project
cd my_python_project
poetry init --name my_python_project --dependency requests --no-interaction
mkdir my_module
touch ./my_module/__main__.py
touch ./my_module/__init__.py
curl -o .gitignore https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore
git init
git add .
git commit -m "initial commit"
```

## Add script if yq isn't installed

```bash
cd ~
cd ws
cd my_python_project
echo """
[tool.poetry.scripts]
hello = \"my_module:hello_world\"
""" >> pyproject.toml

git add .
git commit -m "added script to toml"
```


## main < heredoc

```bash
cd ~
cd ws
cd my_python_project
cat << EOF > my_module/__main__.py
def hello_world():
    print("Hello, world!")

if __name__ == "__main__":
    hello_world()
EOF

git add .
git commit -m "added module"
```

## run

```bash
cd ~
cd ws
cd my_python_project
poetry run python -m my_module
```


## install

```bash
cd ~
cd ws
cd my_python_project
poetry install
```
