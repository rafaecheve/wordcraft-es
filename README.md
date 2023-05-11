# ✨✍️ Wordcraft

Wordcraft es un editor de texto impulsado por LLM con énfasis en la escritura de cuentos.

[g.co/research/wordcraft](http://g.co/research/wordcraft)

Wordcraft es una herramienta construida por investigadores de Google
[PAR](https://pair.withgoogle.com/) para escribir historias con IA. El
La aplicación está impulsada por LLM como
[PaLM](https://developers.generativeai.google/), una de las últimas generaciones de
grandes modelos de lenguaje. En esencia, los LLM son máquinas simples: están capacitados para
predecir la próxima palabra más probable dada una indicación textual. Pero debido a que el modelo
es tan grande y ha sido entrenado en una gran cantidad de texto, es capaz de aprender
conceptos de nivel superior. También demuestra una capacidad emergente fascinante
a menudo referido como
[_aprendizaje en contexto_](https://huggingface.co/blog/few-shot-learning-gpt-neo-and-inference-api).
Al diseñar cuidadosamente las indicaciones de entrada, se puede instruir al modelo para que realice una
increíblemente amplia gama de tareas.

Sin embargo, este proceso (a menudo denominado _ingeniería rápida_) es quisquilloso y
difícil incluso para los practicantes experimentados. Creamos Wordcraft con el objetivo
de explorar hasta dónde podríamos llevar esta técnica a través de un proceso cuidadosamente diseñado
interfaz de usuario, y empoderar a los escritores dándoles acceso a estos
herramientas de última generación.

# 👷‍♂️ Construir

```bash
npm i
npm run dev
```

# ☁️ API

Para ejecutar Wordcraft, necesitará una clave API GenAI. Por favor sigue el
instrucciones en
[developers.generativeai.google/tutorials/setup](https://developers.generativeai.google/tutorials/setup).
Una vez que tenga su clave API, cree un archivo .env y agregue la clave.

```bash
toque .env
echo "API_KEY=\"<INSERT_GENAI_API_KEY>\"" > .env
```

Recuerde, use sus claves API de forma segura. No los comparta con otros, ni incruste
directamente en código que está expuesto al público! Esta aplicación
almacena/carga claves API en el cliente para facilitar el desarrollo, pero estas deben ser
eliminado en todas las aplicaciones de producción!

Puede encontrar más información sobre la API de PaLM 2 en
[developers.generativeai.google](https://developers.generativeai.google/)

# 🤖 Aplicación

Wordcraft se puede personalizar agregando modelos adicionales o agregando
operaciones/controles. La arquitectura básica permite una gran cantidad de
flexibilidad en el

### `/aplicación/contexto`

Define los datos/ejemplos subyacentes que se utilizarán para construir pocos disparos
instrucciones al modelo de lenguaje subyacente. Estos datos de ejemplo pueden ser
personalizado para adaptarse a un estilo o género en particular.

### `/aplicación/núcleo/operaciones`

Define cómo se combina la intención del usuario con el estado del documento, gestiona
actualizar el editor de texto y maneja las opciones del usuario.

### `/aplicación/modelos`

Define cómo se combinan los datos del `Contexto` con un estado de `Operación` para
construye el texto que se enviará a un modo y analiza la salida del modelo.

## Agregar nuevos controles

Para agregar un nuevo control personalizado (por ejemplo, un botón que se traduce en cerdo latino):

- Crear un nuevo `PigLatinExamples` en `/app/context/examples`
- Cree un controlador de solicitud correspondiente en `/app/models/genai/prompts`
- Registre ese controlador de avisos con la clase 'Modelo' subyacente en
   `/app/modelos/genai/index.ts`
- Crear una nueva `PigLatinOperation` en `/app/core/operations`
- Registrar la operación en `main.ts`

<hr />

**Este no es un producto de Google compatible oficialmente**
