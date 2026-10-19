APUNTES GIT  
GitHub Actions y GitHub Pages y Git Ignore

***RESUMEN RAPIDO***

## **1\. Fase Local: Creación y Primeros Archivos (git init \+ .gitignore \+ commit)**

Antes de subir nada a internet, preparas la casa en tu ordenador.

* **Concepto:** Creas el repositorio y decides qué archivos **no** quieres que se guarden (como contraseñas, dependencias, carpetas temporales).  
* **Comandos clave y ejemplo:**  
* Bash

\# 1\. Inicializar git en la carpeta  
git init

\# 2\. Crear un archivo .gitignore para ignorar cosas (ej: node\_modules o .env)  
touch .gitignore  
\# (Dentro de .gitignore escribirías: node\_modules/)

\# 3\. Añadir archivos al "escenario de preparación"  
git add .

\# 4\. Guardar la foto oficial (Commit)  
git commit \-m "Primer commit: estructura inicial"

*   
* 

## **2\. Fase de Ramas y Control de Errores (branch, reset y revert)**

Trabajas en paralelo y aprendes a solucionar cagadas o viajar en el tiempo.

* **Concepto de Ramas:** Creas caminos paralelos (feature, dev, main) para no romper el código principal.  
* **Concepto de Errores (reset vs revert):**  
  * git reset: Borra commits hacia atrás (como si nunca hubieran pasado). ¡Cuidado si ya has hecho push\!  
  * git revert: Crea un commit nuevo que "deshace" los cambios del commit anterior de forma segura (ideal si ya lo has subido a GitHub).  
* **Comandos clave y ejemplo:**  
* Bash

\# Crear y cambiarte a una rama nueva  
git checkout \-b mi-nueva-rama   \# (o git switch \-c mi-nueva-rama)

\# Volver a main y fusionar  
git checkout main  
git merge mi-nueva-rama

\# Viajar en el tiempo (Ejemplo de revert para anular un commit chungo)  
git revert \<codigo-del-commit\>

*   
* 

## **3\. Fase de Conexión a la Nube (git remote add \+ push)**

Vinculas tu ordenador con GitHub por primera vez.

* **Concepto:** Construyes el puente entre tu ordenador y la nube. (Recuerda: esto solo se hace una vez por proyecto).  
* **Comandos clave y ejemplo:**  
* Bash

\# Vincular el repositorio remoto  
git remote add origin https\://github.com/tu-usuario/tu-repositorio.git

\# Subir tus ramas a GitHub por primera vez  
git push \-u origin main

*   
* 

## **4\. Fase de Automatización (GitHub Actions y YAML)**

Configuras tus robots para que trabajen por ti cuando haces push.

* **Concepto:** Creas una carpeta oculta con un archivo .yml que le dice a GitHub qué hacer automáticamente (pasar tests, compilar, etc.).  
* **Estructura y pasos:**  
  1. Creas la ruta: mkdir \-p .github/workflows  
  2. Creas el archivo YAML: touch .github/workflows/deploy.yml  
  3. Contenido básico del archivo YAML:  
  4. YAML

name: Mi Workflow de Examen  
on: \[push\] \# Se dispara cada vez que haces push  
jobs:  
  tarea:  
    runs-on: ubuntu-latest  
    steps:  
      \- name: Checkout del código  
        uses: actions/checkout@v3  
      \- name: Imprimir mensaje  
        run: echo "¡El robot de GitHub ha ejecutado esto solo\!"

5.   
   6.   
   7. Haces git add, git commit y git push de este archivo para que empiece a funcionar en la pestaña *Actions* de GitHub.

## **5\. Fase de Despliegue (GitHub Pages)**

Publicas tu web al mundo entero.

* **Concepto:** Conviertes tus archivos estáticos en una web pública y accesible mediante URL.  
* **Cómo se hace:**  
  * Vas a tu repositorio en GitHub $\rightarrow$ **Settings** $\rightarrow$ **Pages**.  
  * Seleccionas la fuente de despliegue (la rama main o mediante un workflow automatizado si tu examen lo pide así).  
  * ¡Te da una URL y listo\!

***Doc1:***  
SISTEMES DE CONTROL DE VERSIONS

# **📚 Apuntes: Sistemas de Control de Versiones y Git**

## **1\. Conceptos Fundamentales y Terminología**

* **Sistema de Control de Versiones (SCV):** Sistema que registra los cambios realizados en uno o varios archivos a lo largo del tiempo para poder recuperar versiones específicas más adelante.  
* **Repositorio (Repository):** Lugar donde se guardan los archivos actuales y todo el historial de cambios.  
* **Tronco / Rama Principal (*Trunk* / *Master* / *Main*):** Branca principal del repositorio desde la cual se bifurcan las demás.  
* **Rama (*Branch*):** Bifurcación independiente del código que permite desarrollar nuevas funcionalidades o corregir errores sin afectar al tronco principal ni a otras ramas.  
* **HEAD / Capçalera:** Puntero que referencia a la versión o *commit* más reciente de la rama en la que se está trabajando.  
* **Copia de trabajo (*Working copy*):** Copia local de los archivos en la que el usuario realiza modificaciones antes de enviarlas al repositorio.  
* **Commit / Check-in:** Guardar localmente una instantánea de los cambios realizados en el repositorio.  
* **Checkout:** Cambiar de rama o recuperar una versión específica en la área de trabajo.  
* **Pull:** Copia y fusiona los cambios de un repositorio (usualmente remoto) en la copia local.  
* **Push:** Envía las confirmaciones (*commits*) del repositorio local al remoto.  
* **Fetch:** Descarga los cambios del repositorio remoto al local sin fusionarlos automáticamente con el trabajo actual.  
* **Conflict (Conflicto):** Situación que ocurre cuando dos usuarios modifican las mismas líneas de un archivo y el sistema no puede fusionar las diferencias de forma automática.  
* **Merge (Fusionar):** Combinar los cambios de dos ramas independientes en una sola.  
* **Tag / Etiqueta:** Marca o alias que se asigna a un *commit* concreto para identificar hitos o versiones de lanzamiento (ej. v1.0).  
* **Fork:** Creación de una copia independiente de un repositorio en otro servidor/cuenta.  
* **Clone:** Descarga de una copia completa e idéntica de un repositorio existente.


## **3\. Arquitectura y Estados en Git**

### **🔄 Los 3 Estados de los Archivos en Git**

1. **Modificado (*Modified*):** El archivo ha sido cambiado en el directorio de trabajo pero aún no se ha marcado para guardar.  
2. **Preparado (*Staged* / *Staging Area*):** Los archivos modificados se han marcado para ser incluidos en la próxima confirmación.  
3. **Confirmado (*Committed*):** Los datos están almacenados de forma segura en la base de datos local de .git.

### **🛠️ Las 3 Áreas de Trabajo**

* **Working Directory:** Directorio local donde se modifican físicamente los archivos.  
* **Staging Area (Index):** Zona intermedia donde se agrupan las modificaciones preparadas para el *commit*.  
* **Git Directory (.git):** Base de datos que almacena la metainformación y los objetos del repositorio.

## **4\. Comandos Clave de Git**

### **Configuración e Inicialización**

* git config \--global user.name "Tu Nombre": Configura el nombre del usuario a nivel global.  
* git init: Inicializa un nuevo repositorio Git dentro del directorio actual (crea la carpeta oculta .git).  
* git clone \<URL\>: Clona un repositorio remoto completo a tu equipo.

### **Flujo de Trabajo Básico**

* git status: Muestra el estado de los archivos (rastreados, modificados, en staging, etc.).  
* git add \<archivo\> / git add .: Pasa los archivos del directorio de trabajo al *Staging Area*.  
* git commit \-m "Mensaje del commit": Registra una instantánea de los cambios acumulados en el *Staging Area*.  
* git log / git log \--oneline: Muestra el historial cronológico de los *commits* realizados.  
* git rm \<archivo\>: Elimina un archivo del área de seguimiento y del disco.

### **Trabajo con Ramas (*Branches*)**

* git branch: Lista las ramas locales disponibles.  
* git branch \<nombre\_rama\>: Crea una nueva rama apuntando al *commit* actual.  
* git checkout \<nombre\_rama\>: Cambia la copia de trabajo a la rama seleccionada.  
* git checkout \-b \<nueva\_rama\>: Crea la rama y cambia a ella de forma inmediata.  
* git merge \<rama\>: Unifica la rama especificada dentro de la rama en la que te encuentras posicionado.

### **Sincronización Remota**

* git fetch origin: Descarga las referencias del servidor sin modificar el directorio de trabajo local.  
* git pull origin \<rama\>: Trae los cambios del servidor remoto y los fusiona directamente en la rama activa.  
* git push origin \<rama\>: Sube las confirmaciones locales a la rama remota especificada.

### **Archivos Inexistentes / Ignorados (.gitignore)**

* Permite definir reglas mediante un archivo .gitignore para omitir archivos temporales, binarios o claves privadas que no deben ser rastreados por Git.

## **5\. Estrategia de Ramificación: GitFlow**

Es un modelo de ramificación disciplinado que asigna funciones específicas a distintas ramas en el ciclo de vida del proyecto:

* **Ramas Principales (Permanentes):**  
  * master / main: Contiene exclusivamente código estable listo para producción.  
  * develop: Acumula las últimas características listas para el próximo lanzamiento.

***Doc2:***  
💻 Guía Práctica de Git para Examen (Consola y Comandos)

## **🚀 1\. Configuración e Inicialización**

* **Crear un repositorio local:**

git init → *Crea la carpeta oculta .git en el directorio actual para comenzar a rastrearlo*.

## **📝 2\. Estados y Gestión de Archivos en Local**

### **Flujo de trabajo principal:**

1. **Ver el estado de los archivos:**

git status → *Indica qué archivos están modificados, en el Staging Area o sin seguimiento (untracked)*.

2. **Añadir archivos al Staging Area (git add):**

git add README.md        \# Añade un archivo específico  
git add .              	      \# Añade todos los archivos modificados/nuevos

3. **Confirmar cambios (git commit):**  
4. Bash

git commit \-m "Mensaje explicativo del cambio"

## **🔍 3\. Historial e Inspección**

* **Consultar el historial de commits:**

git log → *Muestra identificador (hash), autor, fecha y mensaje de cada commit*.

## **🚫 4\. Ignorar Archivos (.gitignore)**

Un archivo .gitignore permite definir qué archivos o carpetas no deben ser rastreados por Git.

## 

## **🗑️ 5\. Eliminar y Desplazar Archivos (git rm)**

* **Eliminar archivo del disco y del seguimiento:**

git rm archivo.txt → *Elimina el archivo del directorio de trabajo y lo coloca directo en el Staging Area*.

**🔄 6\. Deshacer Cambios (git reset vs git revert)**

### **A) Usando git reset (Reescribe el historial / Mueve el HEAD)**

* **Quitar un archivo del Staging Area:**

git reset nombreArchivo → *El archivo deja de estar en preparación pero conserva los cambios en el directorio local*.

### **B) Usando git revert (Opción Segura)**

* **Invertir un commit creando uno nuevo:**

git revert \<hash\_commit\> → *No borra el historial existente ni mueve el HEAD. En su lugar, aplica los cambios opuestos y crea un commit nuevo.* **Es la opción más segura**.

## **📌 Resumen visual del ciclo práctico para el examen**

![][image1]

***Doc3:***

# **💻 Guía Práctica de Git (Avanzado, Ramas y Etiquetas)**

## **🌐 1\. Gestión de Repositorios Remotos (git remote)**

* **Clonar un repositorio:**

git clone \<URL\_remota\> → Descarga una copia completa de un repositorio remoto al equipo local.

* **Clonar asignando un nombre personalizado a la carpeta:**

git clone \<URL\_remota\> nombre\_carpeta\_nueva → El directorio de destino pasará a llamarse como indiques.

## **🚀 2\. Sincronización con el Servidor (git push, git pull, git fetch)**

* **Enviar cambios al servidor (git push):**

git push origin main → Sube los cambios confirmados (*commits*) de tu rama local al servidor remoto.

* **Actualizar el repositorio local trayendo y fusionando cambios (git pull):**

git pull origin main → Descarga los cambios del servidor remoto y los fusiona automáticamente en tu rama local. (¡Ojo\! Es obligatorio hacer commit de tus cambios locales antes de ejecutar un pull).

* **Descargar información sin fusionar (git fetch):**

git fetch origin → Descarga los datos del servidor remoto y los ubica en una rama oculta local (remotes/origin/main), pero **no** los fusiona automáticamente con tu código actual, permitiéndote inspeccionarlos antes.

## **🌿 3\. Trabajo con Ramas (git branch y git checkout)**

* **Consultar ramas:**

git branch \-a       \# Muestra todas las ramas (locales y remotas)

* **Crear una nueva rama:**

git branch nom\_nova\_rama → Crea el puntero local pero **no** te posiciona en ella de manera automática

* **Desplazarse entre ramas (git checkout):**

git checkout nom\_branca → Cambia la copia de trabajo a la rama seleccionada.

* **Crear una rama y cambiar a ella en un solo paso:**

git checkout \-b nom\_branca → Crea la nueva rama local y sitúa el puntero de HEAD en ella de forma inmediata.

* **Subir una rama local al servidor remoto:**

git push \-u origin nom\_branca\_creada

* **Eliminar ramas:**

git branch \-d nom\_branca\_creada                \# Elimina la rama localmente  
git push origin \--delete nom\_branca\_creada    \# Elimina la rama del servidor remoto

## **🔀 4\. Fusión de Ramas (git merge)**

* **Fusionar una rama en la actual:**

git merge nom\_rama\_a\_fusionar → Toma las líneas independientes de desarrollo y las integra en la rama receptora en la que te encuentres.

* **⚠️ Pasos previos obligatorios antes de un git merge para evitar problemas:**  
  1. Asegurarte de estar posicionado en la rama receptora (comprobar con git status o cambiar con git checkout).  
  2. Actualizar tanto la rama receptora como la que vas a fusionar usando git pull o git fetch \+ git merge para tener los últimos cambios remotos.

## **🏷️ 5\. Etiquetado (git tag)**

Las etiquetas se utilizan para marcar puntos importantes del historial, como versiones de lanzamiento (v1.0).

* **Listar etiquetas:**

git tag                   \# Lista todas las etiquetas por orden alfabético

* **Crear etiquetas:**

git tag v1.0                                       \# Crea una etiqueta ligera (puntero simple)

* **Compartir etiquetas con el servidor remoto:**

git push origin nom\_etiqueta       \# Sube una etiqueta específica  
git push origin \--tags             \# Sube todas las etiquetas locales que no existan en el remoto

* **Eliminar etiquetas:**

git tag \-d nom\_tag                  \# Elimina la etiqueta localmente  
git push origin :refs/tags/nom\_tag  \# Elimina la etiqueta del servidor remoto

* **Trabajar sobre una versión etiquetada:**

git checkout \-b \<nom\_nova\_branca\> nom\_etiqueta

Como no se puede hacer un checkout directo a una etiqueta para modificarla, se crea una nueva rama a partir de esa etiqueta.

***Doc4:***

# **💻 Guía Práctica: GitHub Pages, Colaboración y Buenas Prácticas**

## **🌐 1\. GitHub Pages (Publicación de Sitios Web)**

GitHub Pages permite alojar sitios web estáticos (con archivos README.md o HTML) directamente desde un repositorio de GitHub.

* Pasos principales para configurarlo:  
  1. Crear un repositorio en GitHub.  
  2. Subir los archivos del sitio web o documentación (se suele usar una rama dedicada llamada gh-pages o la rama principal).  
  3. Ir a **Settings** (Configuración) del repositorio en la web de GitHub.  
  4. Buscar la sección de **GitHub Pages**, seleccionar la rama de origen (*Source*) y la carpeta (por ejemplo, /(root)) y guardar.

## **🤝 2\. Colaboración en Proyectos (Fork y Pull Request)**

### **A) Hacer un Fork (Copiar un repositorio)**

Hacer un *Fork* significa clonar un repositorio ajeno a tu propia cuenta de GitHub para poder experimentar e introducir cambios libremente sin alterar el proyecto original.

* **Vincular el repositorio original como referencia (*upstream*):** Una vez clonado tu *fork* en local, es una buena práctica añadir la ruta del repositorio original con el alias upstream:

git remote add upstream direccion\_repositorio\_original

* Actualizar tu repositorio con los cambios del original:

git fetch upstream  
git checkout master  
git merge upstream

### **B) Hacer un Pull Request (Proponer cambios)**

Una vez modificada tu versión copiada (*fork*), puedes solicitar al autor original que integre tus cambios:

1. Vas a la web del repositorio original y haces clic en **New pull request**.  
2. Configuras el *base repository* (el proyecto original y su rama, ej. master) y el *head repository* (tu *fork* y tu rama modificada, ej. ramaEjemplo).  
3. Rellenas el formulario explicando los cambios y haces clic en **Create pull request**.  
4. Si los mantenedores lo aprueban y fusionan, aparecerá como *Merged* y los cambios se aplicarán con éxito al proyecto principal.

***Doc5:***

# **💻 Guía Práctica: GitHub Actions y CI/CD**

## **🔄 1\. Conceptos de CI/CD (Integración y Despliegue Continuo)**

* **Continuous Integration (CI \- Integración Continua):** Práctica donde los desarrolladores integran código en un repositorio compartidos varias veces al día. Cada integración se verifica con tests automatizados para detectar errores de forma temprana.  
* **Continuous Delivery (CD \- Entrega Continua):** Extensión de la CI que asegura que el código siempre esté listo para ser liberado a producción. Pasa por pruebas automatizadas, dejando el sistema preparado para desplegarse en cualquier momento.  
* **Continuous Deployment (CD \- Despliegue Continuo):** Práctica avanzada donde cada cambio aprobado y verificado de forma automática se despliega directamente a producción **sin intervención humana**.

## **⚙️ 2\. Componentes de GitHub Actions**

Un flujo de trabajo se estructura mediante los siguientes elementos:

* **Workflow (Flujo de trabajo):** Procedimiento automatizado configurable que se añade al repositorio. Se compone de uno o más *jobs* y se activa mediante eventos (como un *push* o *pull request*).  
* **Jobs (Trabajos):** Conjunto de pasos (*steps*) que se ejecutan en el mismo *runner*. Por defecto, los *jobs* de un workflow se ejecutan en **paralelo**.  
* **Steps (Pasos):** Tareas individuales que se ejecutan secuencialmente dentro de un *job*. Pueden ser una *action* o un comando de shell.  
* **Actions (Acciones):** Comandos independientes y reutilizables que se combinan para formar los *steps*. Son el bloque de construcción más pequeño.  
* **Runner:** Servidor virtual o local que tiene instalada la aplicación de GitHub Actions y se encarga de ejecutar los *jobs*.

## **📄 3\. Estructura y Sintaxis de un Workflow (YAML)**

Los archivos de configuración de GitHub Actions se escriben en formato **YAML** y deben almacenarse obligatoriamente dentro del directorio .github/workflows/.

### **Ejemplo básico de Workflow:**

name: primer-ejemplo                           \# Nombre opcional del workflow  
on: \[push\]                                 	   \# Evento que activa el flujo

jobs:  
  check-bats-version:  
    runs-on: ubuntu-latest                    \# Entorno del runner  
    steps:  
      \- uses: actions/checkout@v2             \# Descarga el código del repositorio  
      \- uses: actions/setup-node@v1           \# Configura Node.js  
      \- run: npm install \-g bats              \# Ejecuta comandos de shell  
      \- run: bats \-v                          \# Ejecuta comandos de shell

## **🛠️ 4\. Elementos Clave para Examen (Sintaxis YAML)**

* **name**: Especifica el nombre del workflow que aparecerá en la pestaña de GitHub Actions.  
* **on**: Define los eventos que activan el flujo (ej. push, pull\_request, o filtrado por ramas y etiquetas):

on:  
  push:  
    branches: \[ main \]  
    tags: \[ v1 \]

* **jobs.\<job\_id\>.needs**: Permite gestionar dependencias entre *jobs* para evitar que se ejecuten en paralelo o condicionar su ejecución:

jobs:  
  job1:  
    \# ...  
  job2:  
    needs: job1         \# job2 espera a que job1 termine con éxito  
  job3:  
    if: always()  
    needs: \[job1, job2\] \# job3 se ejecuta siempre que terminen job1 y job2\[

* **runs-on**: Define el sistema operativo de la máquina virtual (ej. ubuntu-latest, windows-latest, macos-latest).  
* **env**: Permite definir variables de entorno a nivel global, de job o de step.  
* **uses vs run**:  
  * uses: Se utiliza para invocar **Actions** predefinidas (de GitHub o de terceros, ej. actions/checkout@v2).  
  * run: Se utiliza para ejecutar **comandos de terminal o scripts de shell** directamente\[cite: 125, 134\].

***Doc6:***

# **💻 Guía Práctica: Custom GitHub Actions (Acciones Personalizadas)**

## **🛠️ 1\. Tipos de Custom Actions**

Las acciones personalizadas permiten empaquetar tareas para reutilizarlas en flujos de trabajo. Existen dos tipos principales:

1. **Docker-container actions:**  
   * El código se empaqueta dentro de un contenedor Docker.  
   * Más consistente y fiable, ya que no hay que preocuparse por las dependencias del sistema.  
   * *Inconvenientes:* Solo se pueden ejecutar en entornos Linux y son más lentas.  
2. **JavaScript actions:**  
   * El código se ejecuta directamente sobre el *runner* utilizando Node.js.  
   * Su ejecución es mucho más rápida. Debe estar implementada en JavaScript puro para garantizar su compatibilidad.

## **📄 2\. El Archivo de Metadatos (action.yml)**

Toda acción personalizada requiere obligatoriamente un archivo de configuración de metadatos llamado action.yml (o action.yaml) en la raíz de su carpeta.

### **Principales campos de configuración**

:

* **name**: Nombre de la acción.  
* **description**: Breve descripción de lo que hace.  
* **inputs**: Parámetros de entrada que recibe la acción.  
  * *Nota práctica:* GitHub convierte automáticamente cada input en una variable de entorno con el formato INPUT\_\<VARIABLE\_NAME\> (en mayúsculas y reemplazando espacios por guiones bajos \_).  
* **outputs**: Datos que la acción devuelve o establece tras su ejecución.  
* **runs**: Define cómo se ejecuta la acción (según sea JavaScript o Docker):  
  * Para **JavaScript** especifica el archivo principal (main: 'index.js' o compilado en dist/index.js).  
  * Para **Docker** especifica el archivo image: 'Dockerfile'.

## **💻 3\. Ejemplo Práctico: JavaScript Action**

### **Pasos para crearla e implementarla:**

1. **Crear el archivo de metadatos** (action.yml):  
2. YAML

name: 'Hello World'

description: 'Greet someone and record the time'

inputs:

  who-to-greet:

    description: 'Who to greet'

    required: true

    default: 'World'

outputs:

  time:

    description: 'The time we greeted you'

runs:

  using: 'node12'

  main: 'dist/index.js'

3.   
4. **Inicializar Node.js e instalar dependencias oficiales de GitHub Actions**:  
5. Bash

npm init \-y

npm install @actions/core

npm install @actions/github

6.   
7. **Escribir la lógica principal** (index.js) utilizando @actions/core para recoger inputs y devolver outputs:  
8. JavaScript

const core \= require('@actions/core');

const github \= require('@actions/github');

try {

    const nameToGreet \= core.getInput('who-to-greet');

    console.log(\`Hello \${nameToGreet}\!\`);

    const time \= (new Date()).toTimeString();

    core.setOutput("time", time);

} catch (error) {

    core.setFailed(error.message);

}

9.   
10. **Compilar el proyecto** (para evitar subir la carpeta node\_modules al repositorio) utilizando ncc:  
11. Bash

npm i \-g @vercel/ncc

ncc build index.js \--license licenses.txt

12.   
13. (Asegúrate de que el campo main en action.yml apunte al archivo compilado, ej: dist/index.js).  
14. **Probar la acción local dentro de un Workflow** (.github/workflows/workflow.yml):  
15. YAML

on: \[push\]

jobs:

  hello\_world\_job:

    runs-on: ubuntu-latest

    steps:

      \- name: Checkout

        uses: actions/checkout@v2

      \- name: Hello world action step

        uses: ./path/to/action/folder    \# Ruta local de tu action

        id: hello

        with:

          who-to-greet: 'Mona the Octocat'

      \- name: Get the output time

        run: echo "The time was \${{ steps.hello.outputs.time }}"

16. 

## **🐳 4\. Ejemplo Práctico: Docker Action**

1. **Crear el Dockerfile**:  
2. Dockerfile

FROM alpine:3.10

COPY entrypoint.sh /entrypoint.sh

ENTRYPOINT \["/entrypoint.sh"\]

3.   
4. **Crear el script de entrada** (entrypoint.sh):  
5. Bash

\#\!/bin/sh \-l

echo "Hello \$1"

time=\$(date)

echo "::set-output name=time::\$time"

6.   
7. **Configurar el action.yml para Docker**:  
8. YAML

name: 'Hello World'

description: 'Greet someone'

inputs:

  who-to-greet:

    required: true

    default: 'World'

runs:

  using: 'docker'

  image: 'Dockerfile'

  args:

9.     \- \${{ inputs.who-to-greet }}

doc7:  
Aquí tienes la **Guía Práctica Resumen (Cheat Sheet) de GitHub Actions** basada en el último documento, explicada en castellano y orientada a los conceptos y sintaxis clave para el examen:

# **💻 Guía Práctica: GitHub Actions Cheat Sheet**

## **📄 1\. Estructura y Sintaxis del Workflow**

* **Ubicación y extensión:** Los archivos de flujo de trabajo deben escribirse en sintaxis YAML (.yml o .yaml) y guardarse obligatoriamente en el directorio .github/workflows/ de tu repositorio. Cada archivo YAML corresponde a un workflow independiente.  
* **Nombre del Workflow (name):** Es el nombre descriptivo que aparecerá en la pestaña de actions de tu repositorio.  
* **Variables de entorno (env):** Se pueden definir mapas de variables de entorno a nivel de workflow, job o step. Existen variables predeterminadas por defecto como GITHUB\_SHA, GITHUB\_REF, GITHUB\_EVENT\_NAME, HOME, etc. Además, se pueden utilizar secretos mediante el contexto secrets.GITHUB\_TOKEN para llamadas a la API o comandos de Git.

## **⚡ 2\. Disparadores (on Event)**

El bloque on define qué evento activa la ejecución del workflow. Puede ser una cadena de texto, un array de eventos o un mapa de configuración detallado:

* **Filtros de ramas y etiquetas (branches / tags):** En eventos como push o pull\_request, permiten seleccionar o excluir (usando el prefijo \! o \-ignore como branches-ignore) las referencias de git que activarán el flujo.  
* **Filtros de rutas (paths):** Especifican qué archivos exactos deben haber sido modificados para que el workflow se ejecute.  
* **Actividades específicas (types):** Acotan la ejecución a acciones concretas (como opened, created, edited, etc.).  
* **Ejecución programada (schedule):** Permite lanzar workflows de forma periódica mediante expresiones cron (ej: cron: '\*/15 \* \* \* \*').

## **🏗️ 3\. Trabajos (jobs Collection)**

Un workflow se compone de uno o más jobs identificados por un job\_id único.

* **Ejecución:** Por defecto, los jobs se ejecutan en **paralelo** a menos que se indique lo contrario. Cada job corre en una instancia limpia y nueva del entorno virtual especificado.  
* **needs:** Identifica qué job o jobs deben completarse con éxito antes de que el actual pueda iniciarse. Si un job de dependencia falla, los jobs que lo necesitan se omiten automáticamente (a menos que usen condicionales).  
* **runs-on:** Define el tipo de máquina virtual anfitriona (ej. ubuntu-latest, windows-latest, macos-latest, versiones específicas como ubuntu-20.04, o ejecutores propios mediante etiquetas como \[self-hosted, linux\]).  
* **container y services:** Permiten ejecutar los pasos dentro de contenedores Docker específicos o levantar servicios adicionales de apoyo (como bases de datos o servidores Redis) de forma automatizada.  
* **timeout-minutes:** Establece el tiempo máximo de ejecución en minutos antes de que GitHub cancele el workflow automáticamente (por defecto: 360).

## **🚶 4\. Pasos del Job (steps)**

Cada job contiene una secuencia secuencial de tareas llamadas *steps*. Cada paso se ejecuta en su propio proceso dentro del entorno virtual y tiene acceso al espacio de trabajo.

* **name:** Etiqueta opcional pero muy recomendada para mejorar la legibilidad de los logs.  
* **uses:** Ejecuta una **Action** existente. Se recomienda encarecidamente indicar siempre la versión mediante una referencia de Git, rama, SHA o etiqueta:  
  * uses: {owner}/{repo}@{ref} para acciones en repositorios públicos.  
  * uses: {owner}/{repo}/{path}@{ref} para acciones en un subdirectorio.  
  * uses: ./path/to/dir para acciones locales en el mismo repositorio.  
  * uses: docker://{image}:{tag} para imágenes alojadas en Docker Hub o registros públicos.  
* **with:** Mapa de parámetros de entrada definidos en el archivo action.yml de la acción. Si la acción está basada en contenedores, se usan parámetros especiales como args (para pasar inputs al ENTRYPOINT) o entrypoint (para sobrescribirlo).  
* **run:** Ejecuta un **programa de línea de comandos** utilizando la shell del sistema operativo. Cada palabra clave run abre un proceso nuevo, y se pueden encadenar varios comandos usando el operador de tubería (|).  
* **if:** Permite aplicar una condición lógica sin necesidad de usar bloques \${{ }} para decidir si un paso debe ejecutarse o no.

## **📊 5\. Estrategias, Contextos y Almacenamiento**

* **Estrategia de Matriz (strategy.matrix):** Permite ejecutar el conjunto de pasos de un job sobre múltiples configuraciones combinadas (por ejemplo, probando varios sistemas operativos o versiones de lenguajes en paralelo). El parámetro fail-fast (por defecto true) cancela todos los jobs en curso si uno de ellos falla.  
* **Contextos y Expresiones (\${{ }}):** Salvo en las condiciones if, las expresiones se escriben siempre dentro de un bloque \${{ }} para evaluar operadores, funciones o acceder a objetos de contexto disponibles como github, job, steps, runner, secrets, strategy y matrix.  
* **Almacenamiento de Artefactos y Caché:**  
  * **Artefactos:** Ficheros generados durante la ejecución que se pueden compartir entre jobs usando las acciones oficiales actions/upload-artifact y actions/download-artifact (disponibles para descarga web durante 90 días).  
  * **Caché:** Para reutilizar dependencias entre ejecuciones (como node\_modules), se utiliza la acción actions/cache configurando rutas (path), claves de búsqueda (key) y claves alternativas de restauración (restore-keys).

[image1]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAloAAABLCAYAAACoTin9AAAdbElEQVR4Xu2dV5guRbWGueeSB49eEZQclQzCgGRQQRSQLElyhk0GUQSFjSKSVXKWKApIzkElJyVnTICKEs5Nn3n78I1rr7/6D7OnJ+z9XbzPTFdVh7+6wlerVlXP8b8ff1wZY4wxxpixZ44cYIwxxhhjxgYLLWOMMcaYlrDQMsYYY4xpCQstY4wxxpiWsNAyxhhjjGkJCy1jjDHGmJaw0DLGGGOMaQkLLWOMMcaYlrDQMsYYY4xpCQstY4wxxpiWsNAyxhhjjGkJCy0zJfnZz35WXXfttR3h8MzTT1cXXXhh9dOf/rQjzhhjjBlPLLRMa3zh85+v/vD733eEjwWLLbZY9e1vf7sjHO65555qm623ruaZZ56OOGMGZdq0adXqq69evffuux1xU4XLL7usro853BjTPhZapjUQOnfcccfI8U477TRmndX222/fKLTg0UcesdAyYwJlbdFFF63+9te/joRtteWWHekmM2eeeWZHfRjL+miMacZCy7RG7Jhg+eWXH7OGfYcddugqtB579NGOjsWY0fDhBx/MUG6Zmt5www070k12Yn384D//GdP6aIxpxkLLzBR/fPbZenT/ta99rfruMcdU3zn66GrFFVesLUpDQ0PV9b/6VZ3uyCOOqIXPOuusU6277rrV3Xff3XEtOP6442oB9fWvf7266aabRsLpGL733e9W6623XrXPPvtUm266aYfQ2njjjespw/3226/68Y9/bKFlBmKjjTaqy/Lmm21WHff971e77bZb9csrrqi+8pWvVCuvvHL1xhtv1GVsySWXrBZaaKG6HEO+Djz5xBP1tbb45jerLbfYohZrhH/80UfVaaedVm3/rW/Vg4Xn/vSnOvz222+vllt22eqySy+tjj7qqGqvvfaqVllllerqq66qDj744GrbbbapNht+rrfffrtOT9rPfvazI+mV9r577x1Jr7Q8yyabbFINDddHjqmLK6ywwkh9bKqLxpixwULLjJqPPvywWm211aofHH989dqrr1bzzz9/ddONN9aCiJEyDTkdldJz3G0E/eorr4yIowfuv7+ab775asHGMeIKMfeP996rj5ddZpkZhNZTTz5Z3fCb34wcn/DDH1pomb558YUXarHD/9dcfXU9VXjqqafW5ZVFFZQl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>