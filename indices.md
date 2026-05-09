Nos ayudan a encontrar la información clave.

Document loaders
Text splitters
Vectorstore (Crea el indice)

🕋 Generación Aumentada de Recuperación (RAG)

Muchas aplicaciones LLM requieren datos específicos del usuario que no forman parte del conjunto de entrenamiento del modelo. La principal forma de conseguirlo es a través de la Generación Aumentada por Recuperación (RAG). En este proceso, los datos externos se recuperan y se pasan al LLM cuando se realiza el paso de generación. .

Retrieval
. LangChain provee de todos los tipos de bloques para aplicaciones RAG. Cada uno, puede requerir de uno o barios de ellos según del requerimiento a desarrollar. . Con ello en mente, LangChain nos presenta etapas para recuperar información a partir de un origen o repositorio documental. .

Cargadores de Documentos (Document Loaders). Los cuales proveen de integraciones para cargar la mayoría de documentos según sea su formato de origen.
Transformadores de Documentos (Document Transformers). Los cuales proveen de interfaces para obtener partes relevantes de los documentos.
Incrustadores de Textos (Text Embedding). Los cuales capturan la semántica de los texto en los documentos, permitiendo una via rápida y eficiente de consulta.
Almacenamiento Vectorial (Vector Stores). Siendo almacenamientos vectoriales donde se puede contener contextos