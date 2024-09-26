# TL;DR

Nedan är script för de delar som man gör i en terminal.

Ha först detta installerat på din dator:

-   [Python](https://www.python.org/downloads/) v3.10+
-   [VSCode](https://code.visualstudio.com/) med "Jupyter"-tillägget från [ms-aitools](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)

Samt följande filassociation för `*.ipynb` registrerad i dina VS Code-settings:

```json
"workbench.editorAssociations": {
    >8
    "*.ipynb": "jupyter-notebook"
    8<
},
```

## Skapa projekt

### Skapa projekt och initera git + ignore

```bash
mkdir my_proj && cd my_proj
cat << 'GITIGNORES' >> .gitignore
.history/
.vscode/
venv/
*.pyc
__pycache__/
GITIGNORES
git init .
```

### Skapa och aktivera venv, och installera minimala dependencies

```bash
python -m venv venv
source venv/bin/activate # .\venv\Scripts\activate i Windows
pip install --upgrade pip
pip install jupyter
```

_(öppna VS Code och koda)_

### Skapa lista av dependencies

```bash
pip freeze > requirements.txt
git add requirements.txt
git commit -m 'register python requirements'
```

## Använd projekt

```bash
# hämta projekt
git clone git@github.com:npup/jupyter-notebooks-med-venv-och-vscode.git && cd jupyter-notebooks-med-venv-och-vscode

# skapa+aktivera venv och installera dependencies:
python -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# (öppna VS Code, välj kernel/venv och koda)
```
