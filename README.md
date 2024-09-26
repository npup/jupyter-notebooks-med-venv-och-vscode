# Jupyter Notebook-miljö i en `venv` och med VS Code

(Det finns också en [TLDR](/TLDR.md).)

För att koda i ett hyfsat kodverktyg istället för i en webbläsare, och för
att också undvika att installera en massa dependencies globalt på sin stackars
dator, har jag gjort så som beskrivs nedan.

## Förutsättningar

Installerat på din dator:

-   [Python](https://www.python.org/downloads/) v3.10+
-   [VSCode](https://code.visualstudio.com/)-kompatibel editor med ["Jupyter"-tillägget från ms-aitools](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)

Tillägget installeras enklast genom att söka efter "jupyter" bland "extensions" direkt i VS Code.

### Fil-associationer

Se till att `.ipynb`-filer hanteras som jupyter notebooks istället för att bara tolkas som json. Öppna VS Codes `settings` (`Cmd+,` på en Mac, eller `Ctrl+,` i Windows/Linux) och se till att filassociationen `*.ipynb` är satt till `jupyter-notebook`:

```json
"workbench.editorAssociations": {
    ------------ >8
    "*.ipynb": "jupyter-notebook"
    8< ------------
},
```

## Parentes: om kernels

Om man vill använda sina notebooks på annat håll, eller med andra språk, kan man behöva skapa _kernels_ och peka ut dem för att köra sina notebooks. I VS Code, och med python, brukar det dock räcka att peka ut sin `venv` - se [steg 2b](#2b-skapa-notebook-och-välj-körmiljö).

Skulle du behöva skapa en _kernel_, för användning i t.ex. JupyterLab eller annan miljö som förväntar sig en, gör man så här (efter att ha skapat `venv` i [steg 1b](#1b-uppdatera-och-installera-nödvändiga-och-andra-paket)):

```bash
pip install ipykernel
python -m ipykernel install --user --name=your_kernel_name
```

Den kan du sedan referera från den miljö du valt.

## HOWTO

### 1. Skapa ett projekt med egen `venv`

#### 1a. Skapa projektmapp med `venv` och aktivera

```bash
mkdir my_jupyter_project && cd my_jupyter_project
python -m venv venv
source venv/bin/activate  # mac/linux
#.\venv\Scripts\activate  # Windows
```

Detta `venv`-directory skall ej committas! Lägg till i ev. `.gitignore`:

```bash
echo venv/ >> .gitignore
```

#### 1b. Uppdatera och installera nödvändiga (och andra) paket

```bash
pip install --upgrade pip     # skönt
pip install jupyter           # behövs
pip install pandas matplotlib # behövs troligen förr eller senare
```

### 2. Öppna och kör projektet i din editor

#### 2a. Öppna VS Code "på plats" och skapa en Notebook

```bash
code .
```

#### 2b. Skapa notebook och välj körmiljö

-   Tryck `Cmd+Shift+P` (macOS) eller `Ctrl+Shift+P` (Windows/Linux)
-   Skriv och välj "Create: New Jupyter Notebook"
-   I den nya notebooken, klicka på "Select Kernel" i övre högra hörnet
-   Välj `Python environments > din_venv`

Nu kan du skapa kod- och andra block i filen du skapade, samt exekvera dem.

Det är skönt att ha en isolerad (per projekt) miljö för att undvika paketkonflikter.
Installera ev. övriga paket i den virtuella miljön.

## Dela projektet med andra

För att dela projektet, skapa en `requirements.txt` där projektets alla dependencies är registrerade:

```bash
pip freeze > requirements.txt
```

och committa denna fil med resten av koden.

## Använd någon annans projekt

När projektet är hämtat genom t.ex. checkout eller nedladdning, skapar
man en ny `venv`, aktiverar den, och installerar dependencies i den
utifrån requirements-filen (t.ex. med detta projekt!):

```bash
python -m venv venv
source venv/bin/activate  # mac/linux
#.\venv\Scripts\activate  # Windows
pip install --upgrade pip # skönt
pip install -r requirements.txt
```

&mdash; och väljer denna `venv` för att köra notebooks i detta projekt ([steg 2b](#2b-skapa-notebook-och-välj-körmiljö)).
