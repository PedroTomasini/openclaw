# 🚀 Deploy no Railway - Guia Rápido

Baseado na documentação oficial: https://docs.openclaw.ai/install/railway

## 1. Configurar no Railway Dashboard

### Variáveis de Ambiente (Obrigatórias)

| Variável | Valor | Descrição |
|----------|-------|-----------|
| `PORT` | `8080` | Porta do serviço |
| `NODE_ENV` | `production` | Ambiente de produção |
| `SETUP_PASSWORD` | `<senha_segura>` | Senha para acessar o wizard de setup |
| `OPENCLAW_STATE_DIR` | `/data/.openclaw` | Diretório de estado |
| `OPENCLAW_WORKSPACE_DIR` | `/data/workspace` | Diretório de workspace |
| `OPENCLAW_PREFER_PNPM` | `1` | Forçar uso do pnpm |

### Passos:

1. **No Railway, vá em Variables**
2. Clique em **Raw Editor**
3. Cole o conteúdo do arquivo `railway.env`
4. Substitua `CHANGE_ME` por uma senha segura para `SETUP_PASSWORD`

## 2. Adicionar Volume (Persistência)

1. Vá em **Settings** → **Volumes**
2. **Mount Path**: `/data`
3. **Size**: 1GB (ou mais se necessário)

## 3. Configurar Rede Pública

1. Vá em **Settings** → **Networking**
2. Ative **HTTP Proxy**
3. Port: `8080`

## 4. Deploy

O deploy acontece automaticamente quando você conecta o repositório!

## 5. Configurar via Web Wizard

Após o deploy, acesse:

```
https://<seu-projeto>.up.railway.app/setup
```

1. Digite sua `SETUP_PASSWORD`
2. Escolha um provider de modelo (OpenAI, Anthropic, etc.) e cole sua API key
3. (Opcional) Adicione tokens de Telegram/Discord/Slack
4. Clique em **Run setup**

## 6. Acessar o Control UI

```
https://<seu-projeto>.up.railway.app/openclaw
```

## 7. Backup e Migração

Para exportar seus dados:

```
https://<seu-projeto>.up.railway.app/setup/export
```

Isso permite migrar para outro host sem perder configurações ou memória.

---

## 🆘 Troubleshooting

**Erro de permissão no /data**
→ Verifique se o volume está montado corretamente em `/data`

**Container reiniciando**
→ Verifique os logs no Railway Dashboard → Deployments → Logs

**Não consegue acessar /setup**
→ Verifique se `SETUP_PASSWORD` está configurado

**Dados perdidos após restart**
→ Verifique se o volume em `/data` está configurado
