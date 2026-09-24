# 🚀 Instruções para Deploy no Render

Deploy do BEAST MARAGAMES em minutos!

---

## ✅ Pré-requisitos

1. **Conta GitHub** (gratuita) - [github.com](https://github.com)
2. **Conta Render** (gratuita) - [render.com](https://render.com)
3. **Git instalado** - [git-scm.com](https://git-scm.com)

---

## 📝 Passo 1: Criar Repositório GitHub

### 1.1 Abrir PowerShell/Terminal na pasta do projeto

```powershell
cd C:\Users\Heliom\Desktop\PROJETOS METRO E SUPORTE\BEAST_MARAGAMES
```

### 1.2 Iniciar Git

```bash
git init
git config user.name "Seu Nome"
git config user.email "seu@email.com"
```

### 1.3 Adicionar arquivos

```bash
git add .
git commit -m "Initial commit: BEAST MARAGAMES - Documentação e Protótipo"
```

### 1.4 Criar repositório no GitHub

1. Acesse [github.com/new](https://github.com/new)
2. Preencha:
   - **Repository name:** `beast-maragames`
   - **Description:** "BEAST MARAGAMES - Plataforma de Arena de Jogos"
   - **Visibility:** Public (para compartilhar)
3. Clique "Create repository"

### 1.5 Conectar repo local ao GitHub

Você verá comandos na tela do GitHub. Execute:

```bash
git branch -M main
git remote add origin https://github.com/SEU_USERNAME/beast-maragames.git
git push -u origin main
```

**Pronto!** Seu código está no GitHub ✅

---

## 🚀 Passo 2: Deploy no Render

### 2.1 Acessar Render

1. Vá para [render.com](https://render.com)
2. Clique "Sign up" (ou "Log in" se já tem conta)
3. Escolha "Continue with GitHub"
4. Autorize o Render a acessar seu GitHub

### 2.2 Criar novo Static Site

1. No dashboard do Render, clique **"New"** (canto superior direito)
2. Escolha **"Static Site"**
3. Selecione o repositório `beast-maragames`
4. Clique **"Connect"**

### 2.3 Configurar deployment

Preencha os campos:

| Campo | Valor |
|-------|-------|
| **Name** | `beast-maragames` |
| **Build Command** | *(deixe em branco)* |
| **Publish directory** | `.` |

5. Clique **"Create Static Site"**

### 2.4 Aguardar deploy

- Render vai fazer build automaticamente
- Você verá os logs em tempo real
- Quando terminar, vai ter uma URL tipo: `https://beast-maragames.onrender.com`

**Pronto!** Seu site está no ar! 🎉

---

## 🔗 Compartilhar Link

Sua URL é pública! Compartilhe com amigos:

```
https://beast-maragames.onrender.com
```

Eles podem:
- 📊 Ver a documentação completa
- 📱 Testar o protótipo navegável
- 📄 Ler os markdowns
- 🎮 Explorar o fluxo completo do app

---

## 🔄 Atualizar Projeto

Sempre que fizer mudanças locais:

```bash
git add .
git commit -m "Descrição da mudança"
git push
```

Render vai fazer redeploy automaticamente! ✨

---

## 🆘 Troubleshooting

### Render diz "Build failed"
- Verifique se `.gitignore` não está excluindo arquivos HTML
- Certifique-se que `index.html` existe na raiz

### Links não funcionam
- Verifique se nomes de arquivos estão corretos (case-sensitive)
- Use `.html` ao invés de `.htm`

### Quero usar domínio próprio
- Render oferece custom domains no plano Pro

---

## 💡 Alternativas (Ainda Mais Fáceis)

Se quiser algo ainda mais simples:

### **Vercel** (Recomendado - ainda mais fácil)
1. Acesse [vercel.com](https://vercel.com)
2. Clique "Import Project"
3. Conecte GitHub
4. Deploy feito!

### **Netlify**
1. Acesse [netlify.com](https://netlify.com)
2. Drag & drop a pasta do projeto
3. Pronto!

### **GitHub Pages** (Mais simples ainda)
1. Já está no GitHub!
2. Vá em Settings → Pages
3. Source: main branch
4. Salve!
5. URL: `https://seu-username.github.io/beast-maragames`

---

## ✅ Checklist Final

- [ ] GitHub account criada
- [ ] Repositório criado com sucesso
- [ ] Código feito push para GitHub
- [ ] Render account criada
- [ ] Static Site conectado
- [ ] Deploy completo
- [ ] URL compartilhada com amigos

---

## 🎓 Pronto!

Seu projeto está no ar e compartilhável! 🚀

**URL:** https://beast-maragames.onrender.com
**Documentação:** Completa e navegável
**Protótipo:** Totalmente interativo

Divirta-se compartilhando com seus amigos! 🎮
