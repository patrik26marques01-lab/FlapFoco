# Como publicar o FlapFoco (tudo pelo celular)

## 1. Criar o repositório no GitHub
1. Abra **github.com** no navegador do celular (ou o app do GitHub) e faça login.
2. Toque no **+** no canto superior direito → **New repository**.
3. Nome: `flapfoco`
4. Marque como **Public** (ou Private, tanto faz).
5. NÃO marque "Add a README" (você já vai enviar os arquivos).
6. Toque em **Create repository**.

## 2. Enviar os arquivos deste projeto
1. Na página do repositório recém-criado, toque em **"uploading an existing file"** (ou **Add file → Upload files**).
2. Extraia o .zip que te enviei e envie **todas as pastas e arquivos** mantendo a mesma estrutura:
   - `www/index.html`
   - `.github/workflows/build-apk.yml`
   - `package.json`
   - `capacitor.config.json`
   - `COMO_PUBLICAR.md`
3. Escreva uma mensagem tipo "Versão inicial com melhorias" e toque em **Commit changes**.

> Dica: se o navegador não deixar enviar pastas inteiras de uma vez, envie primeiro os arquivos da raiz (`package.json`, `capacitor.config.json`), depois crie o caminho `www/index.html` manualmente (o GitHub permite digitar o caminho da pasta no nome do arquivo ao fazer upload) e o mesmo pra `.github/workflows/build-apk.yml`.

## 3. Rodar o build automático
1. Assim que você fizer o commit, o GitHub Actions já dispara sozinho (por causa do `on: push` no workflow).
2. Vá na aba **Actions** do repositório e acompanhe o processo "Build FlapFoco APK".
3. Quando terminar (ícone verde ✅), toque no resultado → em **Artifacts**, baixe o arquivo `flapfoco-apk`.
4. Descompacte e instale o `app-debug.apk` no seu Android (pode precisar permitir "instalar de fontes desconhecidas").

## 4. Antes de publicar na Play Store
- Trocar o ID de teste do AdMob em `capacitor.config.json` pelo seu **App ID real** do AdMob.
- Trocar as chamadas simuladas de `Ads.showRewarded` / `Ads.showInterstitial` no `index.html` pelas chamadas reais do plugin `admob-plus-cordova` (ex: `AdMob.rewarded.show()`), depois de configurar os IDs de unidade de anúncio.
- Gerar um APK/AAB **assinado** (release), não o debug — isso exige criar uma keystore. Se quiser, eu te ajudo a montar esse passo no workflow também.

## O que já vem pronto no código (`www/index.html`)
- Dificuldade progressiva (canos mais rápidos e gap menor a cada 25 pontos)
- 5 skins (1 grátis + 4 compráveis com moedas ganhas jogando ou por vídeo assistido)
- Revive com anúncio recompensado (1s de invencibilidade ao voltar)
- Sons e partículas ao pontuar
- Interstitial a cada 3 game overs (não em todos, pra não incomodar)
- Recorde e moedas salvos localmente
- 3 conquistas (10, 50, 100 pontos) com pop-up
