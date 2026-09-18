# CribIA

Detector propio de texto generado por IA con falsos positivos controlados, en un único HTML.

**App:** https://fborrasumh.github.io/cribia/

En lugar de un modelo genérico, construye un detector adaptado a tu dominio. Subes textos que sabes que son humanos (idealmente anteriores a 2022, del mismo idioma, campo y género que vas a analizar) y los modelos de tu cuenta de OpenAI producen tres variantes de sus fragmentos: generación nueva sobre la misma idea y reescritura intensa, etiquetadas como IA, y corrección ortográfica, etiquetada como humana porque es un uso permitido. Con embeddings de OpenAI y rasgos de estilo entrena en el navegador una regresión logística, separando entrenamiento y calibración por documentos.

El umbral se fija con un método conforme sobre ventanas humanas no vistas: con un 95 % de confianza, la tasa de ventanas humanas marcadas por error no supera el objetivo elegido (5 %, 1 %, 0,5 % o 0,1 %). La app indica cuánto texto humano hace falta para cada objetivo (299 ventanas de calibración para el 1 %; unas 3.000 para el 0,1 %). Un documento solo se declara «uso sustancial de IA probable» si la mitad o más de sus ventanas superan el umbral, y los documentos alejados del dominio de calibración se marcan como fuera de dominio, sin veredicto.

- Ventanas de 100, 150 o 250 palabras; índice de IA como porcentaje de palabras en ventanas marcadas; tira de puntuaciones con el umbral; informe en Markdown.
- Vanilla JS, persistencia en IndexedDB, clave de OpenAI en el navegador (`ia_openai_key`), selector con los modelos de la cuenta, `text-embedding-3-small` o `-large`. Detector exportable e importable en JSON.
- Lee PDF, DOCX, TXT, MD y TEX.

**Limitaciones.** Prioriza no acusar por error frente a detectarlo todo: con umbrales estrictos parte del texto de IA pasa sin marcarse, sobre todo si está editado a mano o procede de modelos no incluidos como generadores. La garantía solo vale dentro del dominio de calibración. Ningún detector prueba por sí solo el uso de IA: úsalo como indicio para hablar con el autor, nunca como única base de una sanción.

Autor: Fernando Borrás Rocher (UMH) · ORCID [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573) · Licencia MIT
