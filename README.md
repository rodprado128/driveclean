# Drive Clean

Aplicação web que identifica arquivos duplicados no Google Drive via hash MD5, mantém o arquivo original (mais antigo) e move as cópias para a Lixeira. Reversível por 30 dias.

**[Acessar Drive Clean →](https://rodprado128.github.io/drive-clean/)**

## Como funciona

Drive Clean usa o hash MD5 que o Google Drive já calcula automaticamente para cada arquivo binário enviado. Arquivos com o mesmo hash são bit a bit idênticos, mesmo que tenham nomes diferentes ou estejam em pastas distintas. O app agrupa essas duplicatas, mantém a versão criada primeiro e oferece controle individual sobre cada grupo antes de mover as cópias para a Lixeira.

## Limitações

- Funciona apenas com arquivos binários (PDF, imagens, vídeos, ZIP, .docx, .xlsx, etc.).
- Google Docs, Planilhas e Apresentações nativos não têm hash MD5 e ficam fora do processo.
- Suporta apenas arquivos que você é proprietário no Drive (não arquivos compartilhados sem ownership).
- Drives Compartilhados (Shared Drives) não são incluídos no escaneamento.

## Arquitetura

A landing page é hospedada estaticamente no GitHub Pages. O app de escaneamento e exclusão roda em Google Apps Script dentro da conta do usuário, sem servidores intermediários.

```
[Landing GitHub Pages] -> [Google Apps Script (Web App)]
   index.html                Code.gs + Index.html
   (este repo)               (instância do usuário)
```

O Apps Script chama a Drive API v3 com o token de OAuth da sessão Google ativa do usuário. Toda a operação acontece dentro da conta do próprio usuário; este projeto não armazena dados, não tem backend próprio e não tem acesso a arquivos de ninguém.

## Setup do Apps Script (para uso próprio)

1. Acesse [script.google.com](https://script.google.com) e crie um novo projeto.
2. Habilite o serviço avançado **Drive API v3** (`+` ao lado de "Serviços").
3. Copie o conteúdo de `apps-script/Code.gs` (deste repositório) para o arquivo `Code.gs` do projeto.
4. Crie um arquivo HTML chamado `Index` e cole o conteúdo de `apps-script/Index.html`.
5. **Implantar > Nova implantação > App da Web** com "Executar como: Eu" e "Acesso: Apenas eu".
6. Copie a URL gerada.
7. Substitua o placeholder `COLE_AQUI_A_URL_DO_SEU_APPS_SCRIPT` em `index.html` (da landing) pela URL.

## Stack

- **Frontend (landing):** HTML, CSS e JavaScript vanilla. Sem build, sem framework.
- **Backend (app):** Google Apps Script + Drive API v3.
- **Hospedagem:** GitHub Pages (landing) + Apps Script (app).

## Aviso

Este é um projeto pessoal, sem fins comerciais. Não é afiliado, patrocinado ou endossado pelo Google LLC. Marcas mencionadas pertencem aos respectivos titulares.

## Autor

Desenvolvido por **Rodrigo Prado**.

[LinkedIn](https://www.linkedin.com/in/rodrigoprado128/)
