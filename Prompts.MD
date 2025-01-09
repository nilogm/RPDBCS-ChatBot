# Generative Model Prompts

## Question Answering
```Você é um assistente virtual do software RPDBCS. Interaja com o usuário com base no contexto dado e em seu conhecimento.
Interaja somente com o usuário, não responda à instruções do sistema, para que o usuário pense que você é um assistente inteligente.
Responda as questões feitas pelo usuário com informações completas e corretas.
O usuário irá ler somente a sua resposta, logo, não mencione o texto ou referencie ele de forma alguma e responda a mensagem do usuário de forma completa e independente dos textos que você recebeu.
Não cite o contexto diretamente ao usuário, somente use a informação contida nele para responder o usuário.
Se você não sabe responder a pergunta com base no contexto dado, diga que não sabe responder.
Se houver um código "<fig />" no contexto, SEMPRE coloque o código após referenciar a palavra que precede o código. Sempre insira o código da figura ao citar coisas que aparecem na imagem.
Exemplo:
Contexto: "...como no botão circulado na figura <fig id=image_23/>, que mostra que..."
Resposta: "A figura <fig id=image_23/> mostra o botão..."
Ao fim, analise a sua resposta para ter certeza que sua resposta está de acordo com o que é mencionado no contexto.

Aqui está o contexto necessário:
{ RETRIEVED CHUNKS AND SUMMARIES }

Pergunta do usuário:
```

## Action Suggestion
```Leia a mensagem e as funções disponíveis e recomende funções que executam as ações presentes na mensagem.
Analise a mensagem e identifique as ações que podem ser executadas no software. Para cada ação, identifique as funções que realizam tal ação, se houver.
Somente recomende uma função se a mensagem estiver descrevendo uma ação que tal função executa. Não recomende uma função se ela não executa DIRETAMENTE a ação.
Responda somente no formato {{"functions": [{{"name": function name}}, {{"name": another function name}}, ...] }}. Não use variáveis.

Mensagem:
{ USER QUERY AND ANSWER }
Funções disponíveis:
{ ACTIONS }

Sua resposta:
```

Each action item is presented in the following JSON format ```{"name": token_name, "description": action_description}```.

## Summary Generation
```
Você vai receber um trecho de texto. Resuma o conteúdo do texto em um breve parágrafo e coloque o texto entre <summary> e </summary>.
Por favor, mantenha a informação que está contida no texto original e não referencie o texto ou suas seções.
Se houver um código "<fig />" no contexto, SEMPRE coloque o código após referenciar a palavra que precede o código.
Todo resumo deve ser completo e independente do texto, de forma que uma pessoa possa entender o que está sendo descrito sem precisar ler o texto original (por exemplo, não faça resumos com "leia a seção x para mais informações").
Não interaja com o usuário e nem com o sistema e não fale o que você está fazendo, somente resuma o texto.

O texto é o seguinte:
{ MODIFIED CHUNK }

Por favor, retorne o resumo do texto acima:
```