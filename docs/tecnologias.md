🧰 Módulo de Tecnologías
Este documento describe las tecnologías utilizadas en Hack4Life y el rol específico de cada una dentro de la arquitectura del sistema.

1. Frontend
Tecnología	Uso en el proyecto
React	Construcción de la interfaz de usuario: vista de login, dashboard operativo (RF-04) y chat conversacional para el personal médico (RF-06).
Vite	Herramienta de build y servidor de desarrollo del frontend; ofrece recarga en caliente (npm run dev) para iterar rápido durante el hackathon.
2. Backend
Tecnología	Uso en el proyecto
Python + FastAPI	Expone la API REST principal: recibe las preguntas en lenguaje natural, las envía al agente LLM, valida/sanitiza la consulta SQL generada (RNF-02) y devuelve el resultado. Se ejecuta con uvicorn main:app --reload en desarrollo.
Node.js	Especificar rol si se mantiene en la arquitectura final: ¿orquesta otro servicio, sirve el frontend en producción, o quedó reemplazado por FastAPI? Ajustar esta fila según lo que realmente se implementó.
Go	Microservicios de alto rendimiento para tareas de baja latencia (ej. cálculo de indicadores del motor de alertas, RF-05) o procesamiento concurrente de datos.
3. Procesamiento de Datos
Tecnología	Uso en el proyecto
Python	Lenguaje base para el módulo de ingesta y limpieza de CSVs (RF-01): validación de nulos, campos vacíos e incongruencias antes de cargar a la base de datos.
Pandas	Librería usada dentro del script de ingesta para leer, limpiar y transformar los archivos .csv/.xlsx antes de insertarlos en SQLite.
4. Persistencia
Tecnología	Uso en el proyecto
SQLite	Base de datos local y ligera que almacena los datos hospitalarios simulados (camas, farmacia, citas, quirófanos) para el entorno de demo/prueba del hackathon.
5. Inteligencia Artificial
Tecnología	Uso en el proyecto
Agente LLM (NL2SQL)	Convierte las preguntas en lenguaje natural del personal médico en consultas SQL de solo lectura (SELECT), ejecutadas en un entorno controlado (RF-02).
Capa de sanitización SQL	Middleware en el backend que bloquea sentencias de escritura (DROP, DELETE, UPDATE, INSERT) antes de ejecutar cualquier consulta generada por el modelo (RNF-02).
6. Requisitos de Entorno
Herramienta	Versión utilizada
Python	Completar con el resultado de python --version
Node.js	Completar con el resultado de node --version
Go	Completar con el resultado de go version
FastAPI	Completar con el resultado de pip show fastapi
uvicorn	Completar con el resultado de pip show uvicorn
7. Justificación de la Elección Tecnológica
FastAPI se eligió por su velocidad de desarrollo, tipado con Pydantic (útil para validar las consultas SQL antes de ejecutarlas) y documentación automática vía /docs, algo valioso bajo la presión de tiempo de un hackathon.
SQLite permite levantar una base de datos funcional sin necesidad de infraestructura adicional (servidor de BD separado), ideal para un entorno de demo.
React + Vite ofrece un ciclo de desarrollo rápido con recarga instantánea, priorizando velocidad de iteración sobre configuración compleja.
