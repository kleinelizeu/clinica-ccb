# Hermes Clínica by CCB

![Demonstração](docs/imagens/demo.gif)

> **Falta o GIF de demonstração.** Grave 15–30s mostrando você pedindo um post pelo Telegram
> e o agente respondendo um comentário/DM no Instagram. Exporte como GIF e salve em
> `docs/imagens/demo.gif` (ferramentas: QuickTime + Gifski, ScreenToGif, ou `asciinema`+`agg`).

## 1. O que é
Um agente que cuida do Instagram da sua **clínica de estética/saúde**: responde dúvidas e mensagens, ajuda a encaminhar agendamentos e cria posts — controlado pelo seu **Telegram**, sem você precisar mexer em código.

## 2. Benefícios
- **Responde na hora, 24/7.** Aquela dúvida das 23h ("dói?", "quanto custa?") não fica sem resposta — e paciente que espera some.
- **Menos tempo no celular.** O agente filtra o básico e só te chama no Telegram quando é alguém querendo agendar ou um caso que precisa de você.
- **Padroniza o atendimento.** Sempre acolhedor, sempre dentro das suas regras — nunca um "depende" mal explicado.
- **Não dá vexame clínico.** Por padrão, nunca dá diagnóstico, indica tratamento nem promete resultado pela internet: convida para a avaliação.
- **Protege dados sensíveis.** Não pede CPF, foto íntima nem dado de saúde no Direct.

## 3. Casos de uso reais
- **"Quanto custa a harmonização?"** — o agente explica que o valor depende da avaliação, passa a referência (se você permitir) e convida para agendar no Direct/WhatsApp. Te avisa no Telegram.
- **"Esse procedimento dói? Tem contraindicação?"** — responde de forma geral e acolhedora, sem diagnosticar, e convida para a avaliação onde tudo é visto caso a caso.
- **Comentário "ficou maravilhosa! 😍"** — responde simpático em público para aquecer o engajamento, sem mandar DM.
- **DM "tive uma reação no local da aplicação"** — não tenta resolver: acolhe, orienta a procurar a clínica e **te avisa imediatamente no Telegram**.
- **"Vocês atendem aos sábados?"** — responde a dúvida operacional e puxa para o agendamento.

Veja os roteiros completos em [docs/CASOS-DE-USO.md](docs/CASOS-DE-USO.md).

## 4. Pré-requisitos
1. Uma **VPS** com o **Hermes Agent já instalado** (Docker **ou** nativo). (Material da CCB.)
2. O Hermes com um **modelo de IA configurado** (`hermes setup`).
3. **Telegram** no celular.
4. Uma conta no **Zernio** (zernio.com) com o **Instagram da clínica conectado**.

## 5. Como instalar (1 comando)
Conecte na sua VPS por SSH e cole:

```bash
curl -fsSL https://raw.githubusercontent.com/kleinelizeu/clinica-ccb/main/install.sh | sudo bash
```

O assistente abre sozinho e te guia. Depois, a qualquer momento:

```bash
hermes-clinica            # roda/continua o assistente
hermes-clinica doctor     # confere tudo e corrige problemas comuns
hermes-clinica info       # mostra endereço do webhook, chave e nome do bot
hermes-clinica contexto   # mostra o texto da sua clínica para colar no bot
```

## 6. Como usar no dia a dia
No Telegram do seu bot, é só pedir em português normal:
- "Crie um post sobre limpeza de pele com uma imagem clean. Me mostra antes de publicar."
- "Responde quem comentou perguntando preço chamando pra avaliação no Direct."
- "Quantas pessoas me mandaram DM hoje querendo agendar?"
- "Muda meu tom de voz pra mais leve e próximo."

## 7. Perguntas frequentes + comandos
**Preciso saber programar?** Não. O assistente faz tudo e explica onde clicar.

**O agente vai diagnosticar paciente?** Não. Por padrão ele nunca dá diagnóstico, indica tratamento nem promete resultado — sempre convida para a avaliação presencial.

**Mexe no meu Hermes que já uso?** Cria um agente **separado** (`clinica`), sem mexer no que você já tem.

**Onde ficam minhas senhas e chaves?** Só na **sua VPS**, em `/root/.clinica-ccb/` (protegida).

**Testei do meu próprio Instagram e não respondeu.** Normal: o Zernio só dispara para **outra** pessoa.

**As respostas pararam.** Rode `hermes-clinica doctor` — costuma detectar e corrigir.

Mais detalhes em [docs/COMO-FUNCIONA.md](docs/COMO-FUNCIONA.md), [docs/CASOS-DE-USO.md](docs/CASOS-DE-USO.md) e [docs/PROBLEMAS-COMUNS.md](docs/PROBLEMAS-COMUNS.md).
