# MantenIA

Asistente inteligente de mantenimiento industrial basado en **RAG (Retrieval-Augmented Generation)** sobre una arquitectura multi-nube: **AWS**, **Oracle Cloud** y **Microsoft Azure**.

MantenIA responde preguntas de técnicos de mantenimiento usando únicamente los manuales técnicos de los equipos, y cita el **manual y la página** de donde proviene cada respuesta. Si la información no está en los manuales, lo indica en lugar de inventarla.

> Proyecto de la materia **Cómputo en la nube** — Universidad Autónoma de Guadalajara.
> Prof. Jairo Samuel Rendón del Carmen.

---

## Arquitectura

| Nube | Rol | Servicios |
|---|---|---|
| **AWS** | Entrada y lógica | Amazon S3 (chat y PDFs), API Gateway, AWS Lambda (Python) |
| **Oracle Cloud** | Conocimiento | Autonomous Database con búsqueda vectorial |
| **Microsoft Azure** | Inteligencia | Azure OpenAI (embeddings y modelo de lenguaje) |

### Flujo de una consulta

1. El técnico escribe su pregunta en el chat web.
2. API Gateway invoca a la función Lambda.
3. Azure OpenAI convierte la pregunta en vector.
4. Oracle devuelve los fragmentos más parecidos en significado.
5. Azure OpenAI redacta la respuesta usando solo esos fragmentos, y el chat la muestra con su fuente.

### Carga de manuales (una vez por manual)

1. Se sube el PDF a S3 y se extrae el texto página por página.
2. El texto se divide en fragmentos y Azure OpenAI genera el vector de cada uno.
3. Cada fragmento, su vector, el nombre del manual y la página se guardan en Oracle.

---

## Estructura del repositorio

```
mantenia/
├── frontend/      Interfaz web del chat (HTML, CSS, JS)
├── lambda/        Función AWS Lambda que orquesta el flujo
├── carga/         Script de carga de manuales a Oracle
├── evaluacion/    Banco de preguntas y resultados
└── docs/          Propuesta, cartel y documentación
```

---

## Configuración

Las claves de acceso **nunca** se suben al repositorio. Cada integrante crea un archivo `.env` local (ignorado por Git) con sus credenciales:

```
# Azure OpenAI
AZURE_OPENAI_ENDPOINT=
AZURE_OPENAI_KEY=

# Oracle Autonomous Database
ORACLE_USER=
ORACLE_PASSWORD=
ORACLE_DSN=
```

> Las instrucciones de instalación y ejecución se completarán conforme avance el proyecto.

---

## Equipo

| Integrante | Rol |
|---|---|
| Walter Silva Gaxiola | Líder de AWS e integración |
| Samantha Henry Gonzalez | Líder de Oracle (datos) |
| Emmanuel Castillo Leyva | Líder de Azure (IA y evaluación) |
| Luis Felipe Ramírez Torres | Líder de documentación, interfaz y cartel |
