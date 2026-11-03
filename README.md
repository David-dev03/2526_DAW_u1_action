# README de entrega — DAW-U1.-Practica001

## Estado de la entrega

* **Estado general:** ENTREGADO
* **Estudiante o integrantes:** David Muñoz Valdés
* **Proyecto intermodular:** Aplicación de Mantenimiento de Vehículos (Módulo de Tienda y Descuentos)
* **Repositorio:** [https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03](https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03)

## 1. Entregable 1 — Repositorio y workflow funcionando

**Estado del entregable 1:** ENTREGADO

* **URL del repositorio:** [https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03](https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03)
* **Visibilidad:** Privado
* **Acceso del profesor:** Al usar GitHub Classroom, la organización y el profesorado tienen acceso administrativo automático al repositorio.
* **Archivo del workflow:** .github/workflows/ci.yml
* **Ejecución correcta de GitHub Actions:** Ver pestaña Actions en el repositorio ([https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03/actions](https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03/actions))
* **Evento que inicia el workflow:** Se inicia mediante los eventos push (a la rama main) y manualmente con workflow_dispatch.

## 2. Entregable 2 — Documentación HTML y en otro formato

**Estado del entregable 2:** ENTREGADO

| Formato | Archivo o ruta dentro de docs/ | Enlace para consultarlo | Cómo se genera o publica |
| --- | --- | --- | --- |
| HTML | docs_codigo/html/main.html | Descargable en artefactos | pdoc src/main.py -o docs_codigo/html |
| Markdown | docs_codigo/md/documentacion.md | Descargable en artefactos | pandoc docs_codigo/html/main.html -o docs_codigo/md/documentacion.md |

* **Generación local comprobada:** Se configuró un entorno virtual (.venv), se activó con source .venv/bin/activate y se instaló pdoc. Al ejecutar los comandos, se verificó la creación de las carpetas docs_codigo/html y docs_codigo/md localmente antes de pasarlo al CI.
* **Cómo se almacenan los resultados:** Como Artefactos de Actions (mediante actions/upload-artifact@v4) empaquetados bajo el nombre documentacion-codigo.
* **Evidencia:** Disponibles para descargar en formato .zip en el resumen de cada ejecución (Run) exitosa en la pestaña Actions.

## 3. Entregable 3 — README del proyecto, proceso y cuestionario

**Estado del entregable 3:** ENTREGADO

### 3.a. Herramientas y comandos

**Estado:** ENTREGADO

| Herramienta o dependencia | Versión | Uso |
| --- | --- | --- |
| Python | 3.10 | Lenguaje fuente y runtime en el workflow |
| pdoc | Última | Generador de la documentación inicial en formato HTML |
| pandoc | Última (apt-get) | Conversor de HTML a Markdown para el multiformato |
| MkDocs (Material) | Última | Generación y despliegue del sitio web estático |

Comandos de instalación de dependencias:
pip install pdoc mkdocs mkdocs-material
sudo apt-get update && sudo apt-get install -y pandoc

Comandos para generar HTML:
mkdir -p docs_codigo/html docs_codigo/md
pdoc src/main.py -o docs_codigo/html

Comandos para generar el segundo formato (Markdown):
pandoc docs_codigo/html/main.html -o docs_codigo/md/documentacion.md

### 3.b. Código fuente documentado

**Estado:** ENTREGADO

* **Estilo de documentación:** Google Style Docstrings
* **Archivo fuente documentado:** src/main.py ([https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03/blob/main/src/main.py](https://www.google.com/search?q=https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03/blob/main/src/main.py))
* **Fragmento con la documentación estructurada:**

Calcula el precio final de un recambio aplicando los descuentos de la app.
Aplica un 10% de descuento automático si el usuario está suscrito al plan premium.
Luego, si hay un cupón promocional válido, resta esa cantidad.
Args:
precio_base (float): El precio original de la pieza.
es_premium (bool, optional): True si el usuario paga la suscripción. Por defecto False.
cupon (str, optional): Código promocional introducido. Por defecto "".
Returns:
float: El precio total redondeado que se va a mandar a la pasarela de pago.

* **Documentación generada a partir de ese fragmento:** Se encuentra empaquetada en el HTML del artefacto y renderizada en la web de MkDocs.

### 3.c. Formatos generados y enlaces

**Estado:** ENTREGADO

* **HTML y Segundo formato:** Descargables desde los Artefactos del repositorio ([https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03/actions](https://github.com/IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03/actions)).
* **Artefactos de GitHub Actions:** Se generan bajo el nombre documentacion-codigo en el Job generar-artefactos-codigo.

### 3.d. Funcionamiento del workflow y colaboración

**Estado:** ENTREGADO

1. **Evento y rama:** Disparado por un push a la rama main.
2. **Preparación del entorno:** Se hace un checkout@v4, se configura Python 3.10 y se instalan dependencias (pdoc mediante pip y pandoc mediante apt-get).
3. **Generación:** pdoc genera el HTML y pandoc lo convierte a Markdown. En un job secundario, MkDocs construye el sitio.
4. **Almacenamiento o publicación:** El código documentado sube como artefacto (upload-artifact@v4). La web se publica usando la acción peaceiris/actions-gh-pages@v4 hacia la rama gh-pages.
5. **Comprobación:** El check verde en la pestaña Actions y la disponibilidad de la web pública confirman el éxito.

**Colaboración con GitHub:** Al automatizar este proceso mediante CI/CD, cualquier miembro del equipo que abra una Pull Request pasará por los checks de este workflow. Las reglas de protección de rama impedirían la fusión de código si la documentación no logra construirse, garantizando consistencia en el proyecto colaborativo.

### 3.e. Mensajes de commit

**Estado:** ENTREGADO

| Hash o enlace | Mensaje real | Qué cambio demuestra |
| --- | --- | --- |
| c4ff3f8 | feat: añade codigo python, mkdocs y workflow de actions | Creación de la estructura base y automatización CI/CD. |
| 7a92eaa | fix: instala pandoc en el servidor de actions | Solución del error de entorno instalando el conversor en la máquina Ubuntu. |

**Justificación:** Los mensajes siguen la convención Conventional Commits (feat:, fix:), están escritos en modo imperativo y describen exactamente qué acción se ha llevado a cabo, facilitando la comprensión del historial.

### 3.f. Acceso, seguridad y SSH

**Estado:** ENTREGADO

* **Permisos del repositorio:** El repositorio es privado, gestionado por la organización del instituto y limitado al alumno y profesorado.
* **Protección de ramas o revisiones:** No configurada explicitamente por el alumno debido a las limitaciones de permisos de la organización, pero controlada por Classroom.
* **Secretos de Actions:** Se utiliza un token efímero automático (${{ secrets.GITHUB_TOKEN }}) para que el bot pueda publicar en la rama gh-pages sin necesidad de exponer credenciales personales.
* **Configuración SSH:** Se generó una clave ed25519 en un equipo macOS (MacBook Air) y su clave pública se añadió a los ajustes SSH de la cuenta personal de GitHub.
* **Prueba SSH:**
lagartijaquejica@MacBook-Air-de-David ~ % ssh -T git@github.com
Hi David-dev03! You've successfully authenticated, but GitHub does not provide shell access.

### 3.g. Clonar y reproducir la generación

**Estado:** ENTREGADO

Pasos para clonar y ejecutar en local:
git clone git@github.com:IES-Rafael-Alberti/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03.git
cd deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03
python3 -m venv .venv
source .venv/bin/activate
pip install pdoc mkdocs mkdocs-material
mkdocs serve

* **Requisitos previos:** Python 3 instalado, Git y conexión SSH configurada.
* **Resultado esperado:** Un servidor local web ejecutándose en [http://127.0.0.1:8000/](https://www.google.com/search?q=http://127.0.0.1:8000/) con la documentación de MkDocs.
* **Cómo volver a ejecutar el workflow:** Haciendo cualquier commit y push a la rama main.

### Cuestionario de evaluación CE a–h

#### CE a. Herramientas de generación

* **Estado:** ENTREGADO
* **Respuesta:** Se utilizó pdoc para procesar el código Python y generar HTML, y MkDocs (Material) para el sitio web estático.
* **Evidencia:** Ver bloque 3.a.

#### CE b. Documentación de componentes

* **Estado:** ENTREGADO
* **Respuesta:** Se ha utilizado el formato Google Style. El bloque de código documentado (calcular_precio_repuesto) detalla Args: y Returns:, que pdoc parsea automáticamente.
* **Evidencia:** Ver bloque 3.b.

#### CE c. Formatos

* **Estado:** ENTREGADO
* **Respuesta:** Se generó un archivo Markdown (.md) adicional. Se consiguió encadenando el comando pdoc con el uso de pandoc para la conversión directa en el pipeline de Ubuntu.
* **Evidencia:** Ver bloque 3.c.

#### CE d. Colaboración

* **Estado:** ENTREGADO
* **Respuesta:** GitHub permite aislar el desarrollo en ramas. Al unirlas mediante Pull Requests, las Actions verifican que la nueva documentación compila sin errores antes de mezclarse con el código principal.
* **Evidencia:** Ver bloque 3.d.

#### CE e. Control de versiones

* **Estado:** ENTREGADO
* **Respuesta:** Son descriptivos e imperativos ("feat: añade...", "fix: instala..."), permitiendo saber con un vistazo al log qué problema exacto soluciona cada commit en el flujo de Actions.
* **Evidencia:** Ver bloque 3.e.

#### CE f. Accesibilidad y seguridad

* **Estado:** ENTREGADO
* **Respuesta:** El repositorio es privado bajo una organización educativa. El despliegue se hace usando un Token secreto nativo y temporal de GitHub, y el acceso local se valida estrictamente por clave asimétrica SSH.
* **Evidencia:** Ver bloque 3.f.

#### CE g. Instalación, configuración y uso

* **Estado:** ENTREGADO
* **Respuesta:** El proceso de instalación y comandos locales se encuentra en la sección 3.g, mientras que las herramientas de CI/CD se listan en la 3.a.

#### CE h. Integración continua

* **Estado:** ENTREGADO
* **Respuesta:** Es CI/CD porque no requiere intervención humana. El evento push activa la Action, que levanta un contenedor Ubuntu, instala entornos, verifica fallos, genera los artefactos y actualiza el sitio web público automáticamente.
* **Evidencia:** Ver bloques 3.d y el historial de Actions.

## 4. Entregable 4 — Publicación obligatoria con MkDocs y GitHub Pages

**Estado:** ENTREGADO

* **URL pública de GitHub Pages:** [https://ies-rafael-alberti.github.io/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03/](https://ies-rafael-alberti.github.io/deaw-2dawa-2627-u01-p06-documentacion-ci-cd-david-dev03/)
* **Workflow de construcción y despliegue:** .github/workflows/ci.yml (Job: desplegar-mkdocs)
* **Acción y rama de publicación:** peaceiris/actions-gh-pages@v4 alojando el código en la rama gh-pages.
* **Ejecución correcta de Actions:** Comprobado; la rama se crea dinámicamente y el sitio carga sin errores.

## Conclusiones

Durante esta práctica he comprendido la diferencia entre documentar localmente y automatizar el proceso de integración continua (CI). Aprender a lidiar con el entorno de servidor (como la ausencia inicial de pandoc) demuestra por qué es importante estandarizar los entornos mediante Actions. Una posible mejora para el workflow sería añadir un Job intermedio de testing automatizado (por ejemplo, con pytest) antes del despliegue en Pages, asegurando que la documentación no solo compila, sino que el código base funciona correctamente.

## Revisión final

* [x] Entregable 1: repositorio accesible y workflow funcionando, con un run visible.
* [x] Entregable 2: HTML y segundo formato generados y accesibles.
* [x] Entregable 3: secciones 3.a–3.g completas, cuestionario CE a–h respondido y evidencias enlazadas.
* [x] Entregable 4: sitio publicado en GitHub Pages y workflow de despliegue comprobado.
