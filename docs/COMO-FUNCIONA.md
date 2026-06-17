# Como funciona (em linguagem simples)

O Hermes Clínica liga três coisas: o **Instagram** da sua clínica, o **Zernio** e o seu **agente Hermes**, com o **Telegram** como seu "painel de controle".

## As duas demonstrações

### Demo 1 — Posts com imagem
Você pede um post pelo Telegram (ex.: "crie um post sobre limpeza de pele com uma imagem clean"). O agente escreve a legenda, gera a imagem e mostra para você aprovar. Aprovou, ele publica no Instagram pelo Zernio.

### Demo 2 — Respostas automáticas
Quando alguém comenta ou manda DM no Instagram da clínica, o Zernio avisa o seu agente na hora (*webhook*). O agente lê, responde seguindo as regras da clínica (sem diagnosticar, convidando para a avaliação) e te manda um resumo no Telegram.

```
Comentário/DM no Instagram
        │
        ▼
     Zernio  ──(internet, HTTPS)──►  seu agente Hermes
        ▲                                  │
        │                                  ├─ responde no Instagram
        └────────── publica posts ◄────────┤
                                           └─ te avisa no Telegram
```

## Por que precisa de "endereço HTTPS"
Para o Zernio falar com o seu agente pela internet, o agente precisa de um endereço seguro (https).

- **Docker:** o Traefik do seu Hermes cria esse endereço automaticamente (estável).
- **Nativo:** usamos o **Cloudflare Tunnel** (cloudflared). Esse endereço pode mudar se a VPS reiniciar — por isso existe o `hermes-clinica doctor`, que detecta o novo e te avisa para atualizar no Zernio.

## Onde ficam suas informações
Tudo que você digita (tokens, chave do Zernio, dados da clínica) fica só na sua VPS, em `/root/.clinica-ccb/`, com acesso restrito. As "instruções de trabalho" do agente você mesmo cola no bot do Telegram para ele guardar na memória.

## Cuidado com dados de paciente
O agente é configurado para **nunca** pedir dados sensíveis de saúde, CPF, fotos íntimas ou senha pelo Direct, e para **não** guardar na memória nomes ou informações de quem entra em contato. Casos de saúde (dor, reação) ele não tenta resolver: te avisa no Telegram.
