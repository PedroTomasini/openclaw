# 🚀 Deploy no Railway - Guia Rápido

## 1. Gerar o Gateway Token

```bash
openssl rand -hex 32
```

Copie o resultado (64 caracteres hexadecimais).

## 2. Obter API Key do Moonshot

1. Acesse: https://platform.moonshot.ai
2. Crie uma conta
3. Gere uma API Key
4. A chave começa com `sk-`

## 3. Configurar no Railway

### Opção A: Importar arquivo
1. No Railway, vá em **Variables**
2. Clique em **Raw Editor**
3. Cole o conteúdo do arquivo `railway.env`
4. Substitua `CHANGE_ME` pelos valores reais

### Opção B: Adicionar uma a uma
| Variável | Valor |
|----------|-------|
| `PORT` | `8080` |
| `NODE_ENV` | `production` |
| `OPENCLAW_GATEWAY_TOKEN` | `<token_gerado_no_passo_1>` |
| `MOONSHOT_API_KEY` | `sk-<sua_chave_moonshot>` |
| `OPENCLAW_STATE_DIR` | `/data/.openclaw` |
| `OPENCLAW_WORKSPACE_DIR` | `/data/workspace` |
| `OPENCLAW_PREFER_PNPM` | `1` |

## 4. Adicionar Volume (Persistência)

1. Vá em **Settings** → **Volumes**
2. **Mount Path**: `/data`
3. **Size**: 1GB (ou mais se necessário)

## 5. Deploy

O deploy acontece automaticamente quando você conecta o repositório!

## 6. Verificar se funcionou

Acesse: `https://<seu-projeto>.up.railway.app/health`

Deve retornar: `{"status":"ok"}`

---

## 📝 Modelos Kimi Disponíveis

Com a configuração acima, você terá acesso a:

- `moonshot/kimi-k2.5` (padrão)
- `moonshot/kimi-k2-0905-preview`
- `moonshot/kimi-k2-turbo-preview`
- `moonshot/kimi-k2-thinking`
- `moonshot/kimi-k2-thinking-turbo`

## 🔧 Configurar Cliente Local

Após o deploy, configure seu cliente OpenClaw:

```bash
openclaw config set gateway.url=https://<seu-projeto>.up.railway.app
openclaw config set gateway.token=<OPENCLAW_GATEWAY_TOKEN>
```

Ou use diretamente:

```bash
openclaw agent --gateway https://<seu-projeto>.up.railway.app --message "Olá!"
```

---

## 🆘 Troubleshooting

**Erro: "Unauthorized"**
→ Verifique se `OPENCLAW_GATEWAY_TOKEN` está correto

**Erro: "No model provider configured"**
→ Verifique se `MOONSHOT_API_KEY` está preenchida corretamente

**Container reiniciando**
→ Verifique os logs no Railway Dashboard → Deployments → Logs

**Dados perdidos após restart**
→ Verifique se o volume em `/data` está configurado
