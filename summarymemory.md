La ConversationSummaryBufferMemory (Memoria de Ventana de Resumen del Búfer en español) es una estrategia que permite a un chatbot mantener un equilibrio entre un resumen completo de la conversación y un uso más eficiente de tokens.

Para el seguimiento de esta clase usa el Notebook 3 en la sección ConversationSummaryBufferMemory.

Primero necesitaremos instalar el módulo tiktoken.


# !pip install tiktoken
Luego, importamos las bibliotecas necesarias y creamos la memoria con un límite de 40 tokens.


from langchain.chains.conversation.memory import ConversationSummaryBufferMemory
from langchain.chat_models import ChatOpenAI
from langchain import OpenAI

llm = OpenAI(model_name='text-davinci-003',
             temperature=0,
             max_tokens = 512,
            verbose=True)

memory = ConversationSummaryBufferMemory(llm=OpenAI(), max_token_limit=40)
Ahora, podemos comenzar la conversación. Observa cómo se mantiene el texto completo de las interacciones recientes y se resume el resto.


conversation_with_summary = ConversationChain(
    llm=llm,
    memory=memory,
    verbose=True
)

conversation_with_summary.predict(input="Que ondi, como etai?")
Nos retorna:


> Entering new ConversationChain chain...
Prompt after formatting:
The following is a friendly conversation between a human and an AI. The AI is talkative and provides lots of specific details from its context. If the AI does not know the answer to a question, it truthfully says it does not know.

Current conversation:

Human: Que ondi, como etai?
AI:

> Finished chain.
 Hola! Estoy bien, gracias. ¿Y tú?
Nota cómo mantiene el prompt enviado por el humano, no hay resumen aún pues no hay pasado de los 40 tokens. Sigamos la conversación:


conversation_with_summary.predict(input="Cuéntame sobre la opresión indígena.")
Nos da:


> Entering new ConversationChain chain...
Prompt after formatting:
The following is a friendly conversation between a human and an AI. The AI is talkative and provides lots of specific details from its context. If the AI does not know the answer to a question, it truthfully says it does not know.

Current conversation:
Human: Que ondi, como etai?
AI:  Hola! Estoy bien, gracias. ¿Y tú?
Human: Cuéntame sobre la opresión indígena.
AI:

> Finished chain.
 La opresión indígena es una realidad que ha existido durante mucho tiempo. Los pueblos indígenas han sido discriminados y marginados por la sociedad dominante. Esto ha llevado a la pérdida de tierras, recursos y derechos, así como a la desigualdad en el acceso a la educación, la salud y otros servicios básicos. Esto ha provocado una gran desigualdad entre los pueblos indígenas y el resto de la sociedad.
La memoria sigue sin llenar 40 tokens por lo que tenemos los prompts tal como eran hasta el momento. Sigamos:


conversation_with_summary.predict(input="Entonces por qué sigue habiendo racismo en la región? Habla coloquial para poderme identificar contigo.")
Nos da:


> Entering new ConversationChain chain...
Prompt after formatting:
The following is a friendly conversation between a human and an AI. The AI is talkative and provides lots of specific details from its context. If the AI does not know the answer to a question, it truthfully says it does not know.

Current conversation:
System: 
The human asks the AI how it is doing. The AI responds that it is doing well, and then the human prompts the AI to speak about Indigenous oppression. The AI explains that Indigenous oppression has been a reality for a long time, leading to the loss of land, resources, and rights, as well as unequal access to education, health, and other basic services, resulting in a large gap between Indigenous peoples and the rest of society.
Human: Entonces por qué sigue habiendo racismo en la región? Habla coloquial para poderme identificar contigo.
AI:

> Finished chain.
 Entiendo. Bueno, el racismo sigue existiendo en la región porque hay una falta de conciencia y comprensión de la historia y la cultura de los pueblos indígenas. Muchas personas no entienden la importancia de la cultura indígena y la discriminación que han sufrido durante siglos. Esto ha llevado a una falta de respeto y a una falta de empatía hacia los pueblos indígenas, lo que ha contribuido a la perpetuación del racismo.
Esta vez ya superamos los 40 tokens de la memoria y nos crea un resumen con lo que hemos hablado hasta ahora. A partir de este punto así será.


conversation_with_summary.predict(input="¿Cuál fue la primera pregunta que te hice?")
Retorna:


> Entering new ConversationChain chain...
Prompt after formatting:
The following is a friendly conversation between a human and an AI. The AI is talkative and provides lots of specific details from its context. If the AI does not know the answer to a question, it truthfully says it does not know.

Current conversation:
System: 
The human asks the AI how it is doing. The AI responds that it is doing well, and then the human prompts the AI to speak about Indigenous oppression. The AI explains that Indigenous oppression has been a reality for a long time, leading to the loss of land, resources, and rights, as well as unequal access to education, health, and other basic services, resulting in a large gap between Indigenous peoples and the rest of society. The AI further explains that racism in the region continues to exist because of a lack of awareness and understanding of Indigenous history and culture, and a lack of respect and empathy towards Indigenous peoples, which has contributed to the perpetuation of racism.
Human: ¿Cuál fue la primera pregunta que te hice?
AI:

> Finished chain.
 Me preguntaste cómo me iba. Respondí que me iba bien.
En resumen, este tipo de memoria nos es útil cuando planeamos tener pocas interacciones con el usuario (quizás hasta 100 tokens), pero existe una posibilidad de que la conversación se alargue.

Reto 🏆

Te reto a explorar más con este tipo de memoria. Intenta jugar con diferentes límites de tokens y observa cómo se comporta el bot. Además, experimenta con distintos prompts para ver cómo pueden afectar las respuestas del bot.