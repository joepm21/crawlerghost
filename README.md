# 🕷️ CrawlerGhost

**CrawlerGhost** es una herramienta desarrollada en Python para realizar crawling web y recolectar URLs internas de un dominio objetivo. Está orientada a tareas de reconocimiento en auditorías de seguridad, pentesting web y análisis de superficie de exposición, siempre en entornos autorizados.

La herramienta permite rastrear enlaces internos, separar URLs del dominio principal y subdominios, controlar la profundidad del crawling, definir concurrencia, guardar resultados en un archivo de salida y ejecutar un modo alternativo de compatibilidad mediante `requests`, `mechanicalsoup` y `BeautifulSoup`.

---

## 🚀 Características principales

* Crawling web de URLs internas.
* Extracción de enlaces desde etiquetas HTML como:

  * `<a href="">`
  * `<link href="">`
  * `<script src="">`
  * `<iframe src="">`
  * `<form action="">`
* Soporte para crawling asíncrono usando `aiohttp` y `asyncio`.
* Modo legacy con `requests + mechanicalsoup + BeautifulSoup`.
* Separación automática de resultados:

  * Dominio principal.
  * Subdominios encontrados.
* Opción para incluir subdominios con `-s`.
* Opción verbose con `-v` para visualizar cada URL analizada.
* Output automático en `urls.txt`.
* Filtro de archivos estáticos como imágenes, CSS, JS, PDFs, ZIPs, videos, fuentes, etc.
* Normalización de URLs para evitar duplicados.
* Pantalla de carga limpia durante la ejecución.
* Banner personalizado estilo hacker.

---

## ⚠️ Uso autorizado

Esta herramienta debe utilizarse únicamente en dominios propios, laboratorios controlados o entornos donde se cuente con autorización explícita.

El autor no se hace responsable por el uso indebido de esta herramienta.

```text
Uso permitido solo con autorización.
```

---

## 📦 Requisitos

* Python 3.8 o superior.
* pip.
* Sistema Linux recomendado: Kali Linux, Parrot OS, Ubuntu o Debian.

---

## 🔧 Instalación

Clona el repositorio:

```bash
git clone https://github.com/joepm21/crawlerghost.git
cd crawlerghost
chmod +x crawlerghost
./crawlerghost
```

Instala las dependencias:

```bash
python3 -m pip install -r requirements.txt
```

En Kali Linux o Ubuntu, si no tienes `pip` instalado:

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv -y
```

Opcionalmente puedes usar un entorno virtual:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

---

## 📜 requirements.txt

```txt
aiohttp>=3.9.0
beautifulsoup4>=4.12.0
lxml>=5.0.0
certifi>=2024.0.0
charset-normalizer>=3.3.0
aiosignal>=1.3.1
attrs>=23.1.0
frozenlist>=1.4.0
multidict>=6.0.0
yarl>=1.9.0
requests>=2.31.0
mechanicalsoup>=1.3.0
urllib3>=2.0.0
```

---

## ▶️ Uso básico

Ejecutar crawling contra un dominio:

```bash
./crawlerghost -t https://example.com/
```

Por defecto, los resultados se guardarán en:

```bash
urls.txt
```

---

## 🕷️ Incluir subdominios

Para permitir que la herramienta también guarde URLs pertenecientes a subdominios encontrados durante el crawling:

```bash
./crawlerghost -t https://example.com/ -s
```

Ejemplo de salida en `urls.txt`:

```txt
[DOMINIO PRINCIPAL]
https://example.com/
https://example.com/login
https://example.com/contact

[SUBDOMINIOS]
https://blog.example.com/
https://portal.example.com/login
```

> Nota: La opción `-s` incluye subdominios encontrados mediante enlaces dentro del sitio. No realiza fuerza bruta DNS ni enumeración pasiva de subdominios como `subfinder`, `assetfinder` o `amass`.

---

## 🔎 Modo verbose

Para ver cada URL analizada en pantalla:

```bash
./crawlerghost -t https://example.com/ -v
```

---

## 📂 Cambiar archivo de salida

```bash
./crawlerghost -t https://example.com/ -o resultados.txt
```

---

## ⚡ Controlar concurrencia

La concurrencia define cuántas peticiones se realizan al mismo tiempo.

```bash
./crawlerghost -t https://example.com/ -c 20
```

Para resultados más estables o evitar saturar el servidor:

```bash
./crawlerghost -t https://example.com/ -c 3
```

---

## 📌 Limitar profundidad

La profundidad define cuántos niveles de enlaces seguirá el crawler.

```bash
./crawlerghost -t https://example.com/ -d 3
```

Usar profundidad sin límite:

```bash
./crawlerghost -t https://example.com/ -d 0
```

---

## 🧩 Modo legacy

CrawlerGhost incluye un modo alternativo usando:

```text
requests + mechanicalsoup + BeautifulSoup
```

Este modo puede ser útil cuando una web responde mejor a un comportamiento más tradicional de navegador simple.

Ejecutar en modo legacy:

```bash
./crawlerghost -t https://example.com/ --legacy
```

Modo legacy con subdominios:

```bash
./crawlerghost -t https://example.com/ --legacy -s
```

Modo legacy con verbose:

```bash
./crawlerghost -t https://example.com/ --legacy -v
```

---

## 🧪 Ejemplos de uso

Crawling básico:

```bash
./crawlerghost -t https://example.com/
```

Crawling con subdominios:

```bash
./crawlerghost -t https://example.com/ -s
```

Crawling con salida personalizada:

```bash
./crawlerghost -t https://example.com/ -o example_urls.txt
```

Crawling con profundidad 5:

```bash
./crawlerghost -t https://example.com/ -d 5
```

Crawling con baja concurrencia:

```bash
./crawlerghost -t https://example.com/ -c 3
```

Crawling mostrando cada URL analizada:

```bash
./crawlerghost -t https://example.com/ -v
```

---

## ⚙️ Opciones disponibles

| Opción                | Descripción                                        |
| --------------------- | -------------------------------------------------- |
| `-t`, `--target`      | Dominio o URL objetivo.                            |
| `-d`, `--depth`       | Profundidad máxima del crawling.                   |
| `-c`, `--concurrency` | Número de peticiones concurrentes.                 |
| `--timeout`           | Timeout por petición en segundos.                  |
| `--max-urls`          | Cantidad máxima de URLs a visitar.                 |
| `-s`, `--subdomains`  | Incluye URLs de subdominios encontrados.           |
| `-o`, `--output`      | Archivo donde se guardan los resultados.           |
| `-v`, `--verbose`     | Muestra cada URL analizada en pantalla.            |
| `--legacy`            | Usa modo compatible con requests + mechanicalsoup. |

---

## 📄 Formato del output

El archivo generado separa los resultados de la siguiente forma:

```txt
[DOMINIO PRINCIPAL]
https://example.com/
https://example.com/about
https://example.com/contact

[SUBDOMINIOS]
https://blog.example.com/
https://portal.example.com/login
```

Si no se encuentran subdominios:

```txt
[SUBDOMINIOS]
No se encontraron URLs de subdominios.
```

---

## 🧠 ¿Por qué pueden variar los resultados?

Los resultados pueden variar entre ejecuciones debido a:

* Concurrencia.
* Timeouts.
* Redirecciones.
* Contenido dinámico.
* Cambios en la web.
* CDN o balanceadores.
* Cookies o sesiones.
* Enlaces cargados condicionalmente.
* Respuestas diferentes del servidor.

Para resultados más estables se recomienda bajar la concurrencia:

```bash
./crawlerghost -t https://example.com/ -c 3
```

---

## 🛡️ Uso en pentesting

CrawlerGhost puede ser útil durante la fase de reconocimiento para:

* Identificar rutas internas.
* Recolectar URLs para pruebas manuales.
* Alimentar otras herramientas de análisis web.
* Detectar secciones expuestas.
* Construir un mapa inicial de navegación.
* Separar rutas del dominio principal y subdominios.

Ejemplo de flujo:

```bash
./crawlerghost -t https://example.com/ -s -o urls.txt
cat urls.txt
```

Luego puedes usar las URLs recolectadas como entrada para otras herramientas de análisis autorizadas.

---

## 👤 Autor

```text
created by gh0s7m4n
```

* Blog: https://pvguard.blogspot.com/
* GitHub: https://github.com/joepm21

---

## 📌 Disclaimer

CrawlerGhost fue creado con fines educativos, auditoría autorizada y apoyo en procesos de pentesting ético.

No utilices esta herramienta sobre sistemas de terceros sin autorización previa. El mal uso de esta herramienta es responsabilidad exclusiva del usuario.

---
