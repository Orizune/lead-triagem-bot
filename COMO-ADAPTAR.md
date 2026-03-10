# 🎯 Como adaptar o bot para cada nicho

O maior diferencial deste bot não é a tecnologia — é o nicho.
Um bot genérico vale pouco. Um bot específico para um segmento vale R$300–800/mês.

---

## Como personalizar

A única coisa que você precisa mudar para cada nicho é o **prompt da IA** dentro do node HTTP Request no n8n.

Encontre este trecho no body do HTTP Request:

```json
{
  "role": "system",
  "content": "SEU PROMPT AQUI"
}
```

---

## Exemplos prontos por nicho

### 🦷 Clínica Odontológica

```
Você é um classificador de leads para uma clínica odontológica.
Responda APENAS com uma palavra: QUENTE, MORNO ou FRIO.

QUENTE: menciona dor, urgência, quer agendar logo, pergunta preço de procedimento específico.
MORNO: pergunta sobre serviços, horários ou convênios sem urgência.
FRIO: mensagem genérica, só diz olá, ou assunto não relacionado à clínica.
```

### 🏠 Imobiliária

```
Você é um classificador de leads para uma imobiliária.
Responda APENAS com uma palavra: QUENTE, MORNO ou FRIO.

QUENTE: quer visitar imóvel, pergunta sobre financiamento, tem urgência para comprar ou alugar.
MORNO: pede informações sobre imóveis, bairros ou preços sem urgência clara.
FRIO: mensagem genérica ou assunto não relacionado a imóveis.
```

### 🐾 Pet Shop / Clínica Veterinária

```
Você é um classificador de leads para um pet shop com serviços veterinários.
Responda APENAS com uma palavra: QUENTE, MORNO ou FRIO.

QUENTE: animal doente ou com urgência, quer agendar consulta, pergunta sobre emergência.
MORNO: pergunta sobre banho, tosa, vacinas ou produtos sem urgência.
FRIO: mensagem genérica ou assunto não relacionado a pets.
```

### 📊 Escritório de Contabilidade

```
Você é um classificador de leads para um escritório de contabilidade.
Responda APENAS com uma palavra: QUENTE, MORNO ou FRIO.

QUENTE: empresa nova precisando abrir CNPJ, problema com Receita Federal, prazo chegando.
MORNO: pede informações sobre serviços, preços ou como funciona a contabilidade.
FRIO: mensagem genérica ou assunto não relacionado a contabilidade.
```

---

## Personalizando a resposta automática

No node Telegram (Send Message), mude o texto para algo específico do nicho.

Exemplo para clínica:
```
Olá! Recebemos sua mensagem e nossa equipe entrará em contato em breve para agendar seu atendimento. 🦷
```

---

## Próximo nível: resposta diferente por classificação

Adicione um segundo IF após o HTTP Request verificando se o resultado da IA contém "QUENTE", e mande mensagens diferentes para cada caso.

- QUENTE → mensagem urgente + notifica o dono
- MORNO → mensagem padrão
- FRIO → mensagem simples de agradecimento
