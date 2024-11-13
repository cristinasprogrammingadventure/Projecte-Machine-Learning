# Documentació del Procés de Recol·lecció de Dades per al Projecte de Subscripcions Bancàries

## 1. Fonts

- **Identificació de fonts**: CRM intern del banc i registre de campanyes de màrqueting. CRM and internal marketing tools as primary sources.
- **Descripció de les fonts**: Les dades del CRM cobreixen informació del client i el seu historial amb el banc, mentre que els registres de campanyes contenen dades sobre la freqüència, resultats i tipus de contacte utilitzat.

## 2. Mètodes de Recol·lecció de Dades

- **Procediments i eines**: Extracció en format CSV del CRM i altres sistemes de dades mitjançant API o exportacions directes programades. Els fitxers es poden emmagatzemar en una base de dades central per a l’anàlisi posterior.
- **Freqüència de recol·lecció**: Periòdica (setmanal, mensual o trimestral), especialment sincronitzada amb el cicle de campanyes de màrqueting. Avui en dia, potser que setmanal o com a molt, mensual. Son carregades is actualitzades de forma periodica per a tindre-les actualitzades eper a campanyes actuals o potencials: setmanal, mensual o trimestral, especialment sincronitzada amb el cicle de campanyes de màrqueting. Avui en dia, potser que setmanal o com a molt, mensual. 
- **Scripts de descàrrega**: amb llibreries com Pandas per carregar els fitxers CSV en l'entorn de treball i validar la coherència de les dades.

**Escriure un Script que inclou:**

- conectar un CRM a una base de dades hipotètica com ara SQLite.
- consultas SQL query per a sol·licitar columnes específiques rellevants per al projecte, amb alguns filtres si fa falta.
- convertir les dades a un DataFrame de Pandas i exportar-lo a com a fitxer CSV (bank_dataset.csv).


```python
import pandas as pd
import sqlite3  # Assuming CRM data is in SQLite for this example

# Connect to CRM database
conn = sqlite3.connect('CRM_database.db')

# Define SQL query to extract necessary data
query = """
SELECT client_id, age, job, marital, education, default, balance, housing,
       loan, contact, day, month, duration, campaign, pdays, previous, poutcome, deposit
FROM clients_data
WHERE contact_method = 'campaign'
"""

# Execute query and store result in DataFrame
df = pd.read_sql_query(query, conn)

# Save DataFrame to CSV for future use
df.to_csv('bank_dataset.csv', index=False)

# Close connection
conn.close()

# Display DataFrame information
print(df.info())

```

## 3. Format i Estructura de les Dades

- **Tipus de dades**: Conté atributs **numèrics** (edat, saldo, durada de les trucades), **categòrics** (ocupació, educació) i **d’intervals de temps** (dia, mes de contacte).
- **Format d'emmagatzematge**: Taules tabulars en format CSV per facilitar l'anàlisi amb eines de ML.

## 4. Limitacions de les Dades

- La sincronització entre dades de CRM i campanyes pot portar a desfasaments en els registres. 
- Poden aparèixer valors "unknown" per camps de contacte quan el client no respon o no s’ha registrat l’informació completa.

## 5. Consideracions sobre Dades Sensibles

- **Tipus de dades sensibles**: Inclou dades personals com direccions, el saldo i historial de préstecs del client, com ara client_id, balance, deposit,
- **Mesures de protecció**: Es requereix anonimització en dades personals i restricció d’accés a les dades sensibles (e.g., hashing el **client_id**) 
- La banca ha d’assegurar el compliment de normatives com la GDPR (General Data Protection Regulation de l'Unió Europea l'any 2018) per a la protecció de la privacitat dels clients. 

-------------------------


## Exportar i guardar els fixters .ipynb + .md a una carpeta

Run a script to save your notebook in the specified directory and export a Markdown file of the notebook content in the same folder.


```python
!pip install nbconvert
```

    Requirement already satisfied: nbconvert in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (7.16.4)
    Requirement already satisfied: beautifulsoup4 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (4.12.3)
    Requirement already satisfied: bleach!=5.0.0 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (4.1.0)
    Requirement already satisfied: defusedxml in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (0.7.1)
    Requirement already satisfied: importlib-metadata>=3.6 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (7.0.1)
    Requirement already satisfied: jinja2>=3.0 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (3.1.4)
    Requirement already satisfied: jupyter-core>=4.7 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (5.7.2)
    Requirement already satisfied: jupyterlab-pygments in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (0.1.2)
    Requirement already satisfied: markupsafe>=2.0 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (2.1.3)
    Requirement already satisfied: mistune<4,>=2.0.3 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (2.0.4)
    Requirement already satisfied: nbclient>=0.5.0 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (0.8.0)
    Requirement already satisfied: nbformat>=5.7 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (5.10.4)
    Requirement already satisfied: packaging in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (24.1)
    Requirement already satisfied: pandocfilters>=1.4.1 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (1.5.0)
    Requirement already satisfied: pygments>=2.4.1 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (2.15.1)
    Requirement already satisfied: tinycss2 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (1.2.1)
    Requirement already satisfied: traitlets>=5.1 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbconvert) (5.14.3)
    Requirement already satisfied: six>=1.9.0 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from bleach!=5.0.0->nbconvert) (1.16.0)
    Requirement already satisfied: webencodings in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from bleach!=5.0.0->nbconvert) (0.5.1)
    Requirement already satisfied: zipp>=0.5 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from importlib-metadata>=3.6->nbconvert) (3.20.2)
    Requirement already satisfied: platformdirs>=2.5 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from jupyter-core>=4.7->nbconvert) (3.10.0)
    Requirement already satisfied: pywin32>=300 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from jupyter-core>=4.7->nbconvert) (305.1)
    Requirement already satisfied: jupyter-client>=6.1.12 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbclient>=0.5.0->nbconvert) (8.6.0)
    Requirement already satisfied: fastjsonschema>=2.15 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbformat>=5.7->nbconvert) (2.16.2)
    Requirement already satisfied: jsonschema>=2.6 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from nbformat>=5.7->nbconvert) (4.23.0)
    Requirement already satisfied: soupsieve>1.2 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from beautifulsoup4->nbconvert) (2.5)
    Requirement already satisfied: attrs>=22.2.0 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from jsonschema>=2.6->nbformat>=5.7->nbconvert) (24.2.0)
    Requirement already satisfied: jsonschema-specifications>=2023.03.6 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from jsonschema>=2.6->nbformat>=5.7->nbconvert) (2023.7.1)
    Requirement already satisfied: referencing>=0.28.4 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from jsonschema>=2.6->nbformat>=5.7->nbconvert) (0.30.2)
    Requirement already satisfied: rpds-py>=0.7.1 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from jsonschema>=2.6->nbformat>=5.7->nbconvert) (0.10.6)
    Requirement already satisfied: python-dateutil>=2.8.2 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from jupyter-client>=6.1.12->nbclient>=0.5.0->nbconvert) (2.9.0.post0)
    Requirement already satisfied: pyzmq>=23.0 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from jupyter-client>=6.1.12->nbclient>=0.5.0->nbconvert) (25.1.2)
    Requirement already satisfied: tornado>=6.2 in c:\users\buba\anaconda3\envs\entorn_ml\lib\site-packages (from jupyter-client>=6.1.12->nbclient>=0.5.0->nbconvert) (6.4.1)
    


```python
import nbformat
from nbconvert import MarkdownExporter

# Paths to save files in the specified directory
notebook_path = "BankingDataset_data-retrieval.ipynb"  # Current Jupyter Notebook file name
markdown_path = "C:/Users/Buba/Documents/CURSOS-PROGRAMACION/IT-Academy/Upskilling-ML-negoci/ML_BankingDataset/BankingDataset_data-retrieval.md"
target_notebook_path = "C:/Users/Buba/Documents/CURSOS-PROGRAMACION/IT-Academy/Upskilling-ML-negoci/ML_BankingDataset/BankingDataset_data-retrieval.ipynb"

# Export notebook to Markdown format and save it to the specified directory
with open(notebook_path, "r", encoding="utf-8") as f:
    notebook_content = nbformat.read(f, as_version=4)
    markdown_exporter = MarkdownExporter()
    markdown_content, _ = markdown_exporter.from_notebook_node(notebook_content)
    with open(markdown_path, "w", encoding="utf-8") as md_file:
        md_file.write(markdown_content)

# Copy the .ipynb file to the target directory
import shutil
shutil.copyfile(notebook_path, target_notebook_path)

print("Files saved successfully.")


```

    Files saved successfully.
    


```python
import os

# Define the directory path
directory = "C:/Users/Buba/Documents/CURSOS-PROGRAMACION/IT-Academy/Upskilling-ML-negoci/ML_BankingDataset"

# List all files in the directory
print("Files in the directory:", os.listdir(directory))

```

    Files in the directory: ['BankingDataset_data-retrieval.ipynb', 'BankingDataset_data-retrieval.md']
    
