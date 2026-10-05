# MLOps: Ingesta Colaborativa de Dataset

Este repositorio contiene la arquitectura para la recolección de imágenes utilizando Git (código) y DVC (datos), conectados a Google Drive. Cada estudiante recolectará datos de entre 5 y 30 personas distintas (aproximadamente 10 fotos por persona).

## Pre-requisitos
* Python 3.10 o superior.
* Git.
* ID de Cliente y Secreto de Cliente (entregados por el profesor).

## Paso 1: Configurar el Entorno

Clona el repositorio y entra a la carpeta:
```bash
git clone [https://github.com/trigoduoc/proyecto-dataset-vision.git](https://github.com/trigoduoc/proyecto-dataset-vision.git)
cd proyecto-dataset-vision
```

Crea y activa un entorno virtual. En Windows (CMD/PowerShell):
```bash
python -m venv .venv
.venv\Scripts\activate
```
*(En Mac/Linux usa `python3 -m venv .venv` y `source .venv/bin/activate`)*

Instala las dependencias:
```bash
pip install -r requirements.txt
pip install --upgrade pyOpenSSL cryptography
```

## Paso 2: Autenticación y Descarga (Pull)

Configura las credenciales locales:
```bash
dvc remote modify --local almacenamiento gdrive_client_id "ID_DEL_PROFESOR"
dvc remote modify --local almacenamiento gdrive_client_secret "SECRETO_DEL_PROFESOR"
```

Descarga el dataset inicial:
```bash
dvc pull
```
*Nota: Se abrirá tu navegador. Inicia sesión con el correo que indicaste al profesor, haz clic en Configuración Avanzada y acepta los permisos.*

## Paso 3: Aportar al Dataset (Push)

Trabajarás en tu propia rama y generarás tus propios archivos para no interferir con el resto de la clase. 

1. Crea una nueva rama con tu nombre y apellido (reemplaza nombre_apellido):
```bash
git checkout -b nombre_apellido
```

2. Ordena las imágenes de tus sujetos:
* IMPORTANTE: Solo se permiten formatos `.jpg`, `.jpeg` o `.png`. Si usas iPhone, desactiva el formato `.heic` o convierte las fotos antes de subirlas.
* Crea una carpeta general con tu nombre dentro de `data/images/` (ejemplo: `data/images/juan_perez/`).
* Dentro de esa carpeta, crea una subcarpeta por cada persona distinta que fotografiaste. Usa tus iniciales y un número para que el ID sea único (ejemplo: `jp_01`, `jp_02`, hasta `jp_30`).
* Pega las 10 fotos correspondientes dentro de la subcarpeta de cada persona.

3. Registra los metadatos:
* Saca una copia del archivo `plantilla_sujetos.csv` y renómbralo con tu nombre (ejemplo: `sujetos_juan_perez.csv`).
* Ábrelo y registra a cada persona (una fila por sujeto). Ejemplo para el sujeto 1:
  - `id_carpeta`: jp_01
  - `nombre_original`: Carlos Gomez
  - `nombre_normalizado`: carlos_gomez

4. Registra TUS imágenes en DVC y súbelas a Drive:
```bash
dvc add data/images/tu_nombre_apellido
dvc push
```

5. Guarda TU registro de DVC y TU archivo CSV en Git:
```bash
git add data/images/tu_nombre_apellido.dvc sujetos_tu_nombre.csv
git commit -m "Agrega imágenes y metadatos de [Tu Nombre y Apellido]"
git push origin nombre_apellido
```

6. Avisa al profesor:
Ve a la página de GitHub del repositorio y haz clic en el botón "Compare & pull request" para entregar tu trabajo.
