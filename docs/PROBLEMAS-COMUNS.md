# Problemas comuns (e como resolver)

A maioria se resolve rodando:

```bash
hermes-clinica doctor
```

---

### "Comentei/mandei DM e o agente não respondeu"
**Quase sempre não é bug.** O Zernio só dispara o webhook para interações de **outra** pessoa. Teste de **outra conta** do Instagram.

### "As respostas pararam de funcionar do nada" (instalação nativa)
O endereço do túnel (Cloudflare) provavelmente **mudou** (a VPS reiniciou). Rode `hermes-clinica doctor`: ele mostra o **endereço novo**. Atualize no painel do Zernio em *Webhooks → seu webhook → Endpoint URL*.

### "O bot do Telegram não responde"
O token pode ter sido revogado no @BotFather. Rode `hermes-clinica` de novo e cole o token atual.

### "O agente respondeu dando um diagnóstico / prometendo resultado"
Não deveria. As regras da clínica (sem diagnóstico, sem promessa, convidar para avaliação) ficam no contexto do negócio. Rode `hermes-clinica contexto`, confira o texto e cole de novo no bot pedindo "salve isso na sua memória". Se persistir, reforce a restrição rodando `hermes-clinica` e ajustando a resposta sobre "o que o agente NUNCA deve fazer".

### "O agente responde 'qual contato? qual interação?'"
A rota do webhook está sem os dados do evento. O assistente cria a rota com o marcador `{__raw__}`. Rode `hermes-clinica doctor` para recriar.

### "O Zernio mostra 200/sucesso, mas o agente não age"
A rota não pode ter **filtro de eventos**. O assistente cria a rota **sem filtro**. Rode `hermes-clinica doctor`.

### "O Zernio mostra 401 (não autorizado)"
A **chave de segurança** (Signing Secret) no painel do Zernio difere da que está na VPS. Rode `hermes-clinica info` para ver a chave certa e cole no Zernio.

### "Depois de atualizar o Hermes, parou" (instalação nativa)
Atualizar o Hermes apaga o ajuste da assinatura (`X-Zernio-Signature`). Rode `hermes-clinica doctor` — ele reaplica.

### "A resposta demora vários minutos"
Depende do modelo de IA configurado no seu Hermes. Modelos gratuitos costumam ser mais lentos. Configure um modelo mais rápido no perfil.

---

Se nada disso resolver, leve a saída do `hermes-clinica doctor` para a comunidade.
