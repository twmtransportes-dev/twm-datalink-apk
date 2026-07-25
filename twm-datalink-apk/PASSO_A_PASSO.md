# TWM DataLink — APK gratuito, compilado na nuvem

Este projeto gera um APK **de graça**, compilado pelo GitHub (sem instalar nada no PC).
O APK carrega TODOS os módulos direto do site — então continua atualizando sozinho
quando você mexe no GitHub. O que ele adiciona é o **GPS em segundo plano**, que
transmite mesmo com o app fechado.

═══════════════════════════════════════════════════════════════════
COMO FUNCIONA (visão geral)
═══════════════════════════════════════════════════════════════════
- O APK abre o site twmtransportes-dev.github.io (todos os módulos vêm de lá).
- Em paralelo, roda um GPS nativo que envia a posição para o mesmo Apps Script
  que o site já usa — com o app aberto OU fechado.
- Nada muda no backend nem nos outros módulos. É 100% integrado com o site do PC.

═══════════════════════════════════════════════════════════════════
PASSO 1 — Criar o repositório do APK
═══════════════════════════════════════════════════════════════════
1. No GitHub, clique em "New repository".
2. Nome: twm-datalink-apk
3. Deixe PÚBLICO (ou privado, tanto faz).
4. Crie o repositório vazio (sem README).

═══════════════════════════════════════════════════════════════════
PASSO 2 — Subir os arquivos deste projeto
═══════════════════════════════════════════════════════════════════
Suba estes arquivos/pastas para o repositório (mantendo a estrutura):

  .github/workflows/build-apk.yml   ← compila o APK na nuvem
  www/index.html                    ← inicia o GPS e abre o site
  capacitor.config.json             ← configuração do app
  package.json                      ← dependências
  .gitignore

Como subir pelo navegador:
1. No repositório, clique em "Add file" → "Upload files".
2. Arraste os arquivos. Para a pasta .github/workflows, crie o caminho
   digitando ".github/workflows/build-apk.yml" ao criar o arquivo.
3. Commit.

(Se preferir, dá para usar o GitHub Desktop e arrastar a pasta inteira.)

═══════════════════════════════════════════════════════════════════
PASSO 3 — Rodar a compilação
═══════════════════════════════════════════════════════════════════
1. No repositório, vá na aba "Actions".
2. Se pedir, clique em "I understand my workflows, enable them".
3. Clique no workflow "Gerar APK TWM" → botão "Run workflow" → "Run workflow".
4. Espere de 5 a 10 minutos (o GitHub está compilando na nuvem).
5. Quando terminar (✓ verde), clique na execução.
6. Em "Artifacts" (embaixo), baixe "TWM-DataLink-APK".
7. Dentro do zip está o app-debug.apk.

═══════════════════════════════════════════════════════════════════
PASSO 4 — Instalar no tablet
═══════════════════════════════════════════════════════════════════
1. Passe o .apk para o tablet (WhatsApp, cabo, Google Drive...).
2. No tablet: Configurações → Segurança → ative "Fontes desconhecidas"
   (ou permita a instalação quando o Android perguntar).
3. Abra o .apk e instale.
4. Na primeira abertura, o app vai pedir permissão de localização:
   escolha "PERMITIR O TEMPO TODO" — é isso que faz o GPS rodar com o app fechado.
5. Configure a VP do tablet normalmente (⚙️ no mapa), igual ao site.

═══════════════════════════════════════════════════════════════════
COMO ATUALIZAR DEPOIS
═══════════════════════════════════════════════════════════════════
- Mudou algum MÓDULO (checklist, manutenção, mapa...)? Só atualize o site no
  GitHub como sempre. O APK pega automaticamente — NÃO precisa gerar APK novo.
- Só precisa gerar APK novo se mudar algo no PRÓPRIO app (o GPS nativo, o ícone).

═══════════════════════════════════════════════════════════════════
OBSERVAÇÕES IMPORTANTES
═══════════════════════════════════════════════════════════════════
- Este APK é "debug" (para uso interno). Instala e funciona normalmente.
  Para publicar na Play Store seria preciso assinar — mas para uso na empresa,
  instalando direto nos tablets, o debug serve perfeitamente.
- Bateria: no tablet, desative a "otimização de bateria" para o TWM DataLink
  (Configurações → Apps → TWM DataLink → Bateria → Sem restrições).
  Sem isso, o Android pode pausar o GPS depois de um tempo.
- Mesmo assim, nenhum app transmite 100% absoluto se o tablet desligar ou
  ficar sem sinal. Mas com "permitir o tempo todo" + bateria sem restrição,
  fica muito próximo disso.

═══════════════════════════════════════════════════════════════════
SE DER ALGUM ERRO NA COMPILAÇÃO
═══════════════════════════════════════════════════════════════════
- Na aba Actions, clique na execução que falhou (✗ vermelho) e veja em qual
  passo parou. Me mande o texto do erro que eu ajusto.
- O erro mais comum é o Gradle na primeira vez — costuma resolver rodando
  o workflow de novo.
