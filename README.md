# edu_python_intro_poetry

[Poetry](https://python-poetry.org)
[toml](https://toml.io/en/)  
[yq](https://github.com/mikefarah/yq)  

## instructions

> Requires yq is installed

```bash
mkdir my_python_project
cd my_python_project
poetry init --name my_python_project --dependency requests --no-interaction
yq -i '.tool.poetry.scripts.hello = "my_module:hello_world"' pyproject.toml
mkdir my_module
touch ./my_module/__main__.py
touch ./my_module/__init__.py
poetry install
```

## Add script if yq isn't installed

```bash
echo """
[tool.poetry.scripts]
hello = \"my_module:hello_world\"
""" >> pyproject.toml
```


## main < heredoc

```bash
cat << EOF > my_module/__main__.py
def hello_world():
    print("Hello, world!")

if __name__ == "__main__":
    hello_world()
EOF
```

## run

```bash
poetry run python -m my_module
```


## install

```bash
poetry install
```
