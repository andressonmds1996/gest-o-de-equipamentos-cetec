# 🖥️ Suporte TI — Cetec Palmas
### Sistema de Gestão de Equipamentos

Sistema web para solicitação e gestão de equipamentos de TI, desenvolvido para uso interno da **Cetec Palmas**. Colaboradores solicitam equipamentos através de um formulário online, enquanto o técnico e a gerente gerenciam os pedidos por interfaces dedicadas.

---

## ✨ Funcionalidades

### 👤 Portal do Colaborador (`index.html`)
- Formulário em 3 etapas com validação em tempo real
- Seleção múltipla de equipamentos com carrinho dinâmico
- Equipamentos disponíveis: Notebook, Computador, Monitor, Projetor, Mouse, Teclado, Óculos de Realidade Aumentada, Fone de Ouvido e Outros
- Seleção de setor, tipo de atendimento, urgência e tempo de uso
- Termo de compromisso de devolução (exibido apenas quando há prazo em dias)
- Geração automática de número de protocolo (`SOLI-YYYYMMDD-XXXX`)
- Registro automático no banco de dados Supabase
- Envio de e-mail automático ao técnico e confirmação ao solicitante

### 🛠️ Área do Técnico (`tecnico.html`)
- Login com usuário e senha validados no Supabase
- Dashboard com contadores por status (Pendente, Em Análise, Aprovado, Reprovado)
- Listagem completa com filtros e busca
- Modal de detalhes com resposta ao solicitante
- Todos os status disponíveis: Aprovado, Em Análise e Reprovado
- Notificações do navegador para novos pedidos
- Auto-refresh a cada 30 segundos
- **Troca de senha** funciona em qualquer dispositivo

### 🔐 Área da Gerente (`gerente.html`)
- Login com usuário e senha validados no Supabase
- Visualiza apenas solicitações com status **Em Análise**
- Pode somente **Autorizar** ou **Reprovar** pedidos
- Notificações do navegador para novos itens aguardando autorização
- Auto-refresh a cada 30 segundos
- **Troca de senha** funciona em qualquer dispositivo

---

## 🔄 Fluxo do Sistema

```
Colaborador preenche o formulário
        ↓
Protocolo gerado automaticamente
        ↓
Dados salvos no Supabase (PostgreSQL)
        ↓
E-mail enviado ao Técnico + confirmação ao Colaborador
        ↓
Técnico acessa a Área do Técnico
        ↓
Para itens de alto valor → marca como "Em Análise"
        ↓
Gerente acessa e Autoriza ou Reprova
        ↓
Para demais itens → Técnico Aprova ou Reprova diretamente
        ↓
Status atualizado no Supabase
E-mail com a decisão enviado ao Colaborador
```

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Uso |
|---|---|
| HTML5 / CSS3 / JavaScript | Interface do sistema |
| [Supabase](https://supabase.com) | Banco de dados PostgreSQL + API REST |
| [EmailJS](https://www.emailjs.com) | Envio de e-mails sem backend |
| GitHub Pages | Hospedagem gratuita |

---

## 📁 Estrutura do Projeto

```
suporte-ti/
│
├── index.html      # Portal do colaborador
├── tecnico.html    # Área do técnico (gestão completa)
├── gerente.html    # Área da gerente (autorização)
└── README.md       # Documentação
```

---

## ⚙️ Configuração

### 1. Supabase
1. Crie conta em [supabase.com](https://supabase.com) e um novo projeto
2. No **SQL Editor**, execute o script de criação de tabelas (`setup.sql`)
3. Em **Settings → API**, copie a **Project URL** e **anon key**
4. Substitua nos três arquivos HTML:
```javascript
const sb = createClient('SUA_PROJECT_URL', 'SUA_ANON_KEY');
```

### 2. EmailJS
1. Crie conta em [emailjs.com](https://emailjs.com)
2. Conecte seu e-mail e crie um template com `{{name}}`, `{{message}}` e `{{to_email}}`
3. Substitua nos HTMLs:
```javascript
const EMAILJS_KEY = 'SUA_PUBLIC_KEY';
const EMAILJS_SVC = 'SEU_SERVICE_ID';
const EMAILJS_TPL = 'SEU_TEMPLATE_ID';
```

### 3. GitHub Pages
1. Suba os três arquivos HTML no repositório
2. **Settings → Pages → main / (root) → Save**

---

## 🔗 Acesso

| Página | URL |
|---|---|
| Portal do Colaborador | `https://cetec-ti.github.io/suporte-ti` |
| Área do Técnico | `https://cetec-ti.github.io/suporte-ti/tecnico.html` |
| Área da Gerente | `https://cetec-ti.github.io/suporte-ti/gerente.html` |

---

## 👥 Perfis de Acesso

| Perfil | Usuário | Ver todos | Aprovar | Em Análise | Reprovar | Trocar senha |
|---|---|---|---|---|---|---|
| **Técnico** | `andressonmouzinho` | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Gerente** | `neuzelysantos` | ❌ | ✅ | ❌ | ✅ | ✅ |

---

## 📊 SLA — Prazo de Resposta

| Prioridade | Prazo |
|---|---|
| 🔴 Alta | 1 dia útil |
| 🟡 Média | 3 dias úteis |
| 🟢 Baixa | 5 dias úteis |

---

## 🔒 Segurança

- Autenticação validada diretamente no Supabase
- Senhas alteráveis a qualquer momento em qualquer dispositivo
- Perfis com permissões distintas por papel (role)
- EmailJS utiliza apenas chave pública no frontend

---

## 👨‍💻 Desenvolvido por

**Andresson Mouzinho de Sousa**
Suporte TI — Cetec Palmas
Sistema desenvolvido com auxílio de IA — Claude (Anthropic)
