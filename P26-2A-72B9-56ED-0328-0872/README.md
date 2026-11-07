# Projeto #40: Timesheet e Apontamento de Horas em Projetos de Software

- **Modalidade:** Projeto Oficial Sorteado (Valendo 100 pontos)
- **Estudante:** Laura Gois Casteleins
- **Turma:** 2A
- **Chave Única:** `P26-2A-72B9-56ED-0328-0872`
- **URL_CLOUDFLARE:** `https://p26-2a-72b9-56ed-0328-0872.pages.dev` *(Atualize com a URL pública real do seu deploy na Cloudflare antes de abrir o Pull Request)*

---

## Especificação do Projeto

Implemente uma ferramenta de registro de horas trabalhadas para equipes de Engenharia de Software. Autenticado via Discord, o aluno pode iniciar um cronômetro em tempo real ao começar a programar uma funcionalidade ou lançar manualmente um bloco de horas trabalhadas, vinculando o registro à etapa do ciclo de vida (Requisitos, Arquitetura, Codificação, Testes).

Os apontamentos são persistidos no Cloudflare D1. A interface em JavaScript vanilla deve oferecer um painel analítico que soma as horas individuais e da equipe, comparando o tempo estimado inicialmente para cada módulo do projeto com o tempo real efetivamente gasto, destacando desvios de cronograma.

---

## Como Publicar esta Subpasta no Cloudflare Pages + D1 + Discord OAuth2

1. No painel da Cloudflare (**Workers & Pages** → **Create** → **Pages** → **Connect to Git**), selecione o seu fork do repositório `Avalia2026-2`.
2. Configure os parâmetros de build apontando para esta subpasta:
   - **Root directory (Diretório raiz):** `P26-2A-72B9-56ED-0328-0872`
   - **Build command:** *(deixe em branco — HTML/CSS/JS puro)*
   - **Build output directory:** `public`
3. Crie o banco de dados D1 e aplique a migração inicial (no terminal do laboratório usando Scoop):
   ```powershell
   cd P26-2A-72B9-56ED-0328-0872
   npx.cmd wrangler d1 create db-p26-2a-72b9-56ed-0328-0872
   # Copie o database_id gerado para o arquivo wrangler.jsonc e execute:
   npx.cmd wrangler d1 migrations apply DB --remote
   ```
4. **Vincule o Banco D1 ao seu Cloudflare Pages (Obrigatório para ativar env.DB):**
   - No painel da Cloudflare: acesse seu projeto Pages → **Settings** → **Functions** → **D1 database bindings**.
   - Clique em **Add binding**:
     - **Variable name:** `DB`
     - **D1 database:** selecione o banco que você criou (`db-p26-2a-72b9-56ed-0328-0872`).
5. **Configuração do Discord OAuth2 (Obrigatório para autenticação real):**
   - Acesse o **Discord Developer Portal** (https://discord.com/developers/applications) e crie uma nova Application.
   - Na aba **OAuth2**:
     - Copie o **Client ID** e gere o **Client Secret**.
     - Em **Redirects**, adicione a URL exata do deploy:
       `https://p26-2a-72b9-56ed-0328-0872.pages.dev/api/auth/discord/callback`
   - No painel do seu projeto no Cloudflare Pages:
     - Acesse **Settings** → **Environment variables**.
     - Adicione as variáveis de ambiente:
       - `DISCORD_CLIENT_ID`
       - `DISCORD_CLIENT_SECRET`
6. Atualize o campo **URL_CLOUDFLARE** no topo deste `README.md` com o endereço público gerado pela Cloudflare.
7. Na raiz do repositório, execute `node validar-local.mjs P26-2A-72B9-56ED-0328-0872` para validar todos os critérios antes de fazer o commit e abrir o Pull Request.
