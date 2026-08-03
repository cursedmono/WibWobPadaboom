# WibWob Reload

**Documentação : Português do Brasil | [Français](README.md) | [English](README.en.md)**

Servidor local e experimental para a comunidade para **Yo-kai Watch Wibble Wobble**.

> [!WARNING]
> **Apenas a versão em Inglês.** O servidor e o criador de APK suportam somente a versão em inglês do jogo, a opção Francês/Inglês oferecida pelo programa apenas altera o idioma da interface e dos registros, ela não traduz o jogo em si.

> [!CAUTION]
> Este é um projeto não oficial, sem qualquer vínculo, endosso ou parceria com a **LEVEL-5**, **NHN PlayArt** ou **SuperTavor(zura)**. Marcas registradas e conteúdo pertencem aos seus respectivos proprietários. Use e compartilhe apenas arquivos para os quais você possua os direitos necessários.

## Conteúdo da versão

| Elementos | Finalidade |
| --- | --- |
| `LANCER_WIBWOB.bat` | Iniciar o servidor com a configuração de desenvolvimento. |
| `ADMIN_CLIENT/WibWobAdmin.exe` | Administra as contas e o banco de dados local. |
| `CUSTOM_APK_BUILDER/WibWobApkBuilder.exe` | Cria um APK apontando para o servidor local. |
| `WWR_BACKUP/` | Faz um backup do PostgreSQL e dos recursos necessários para o servidor. |
| `appsettings.Development.json` | Modelo de configuração sem senha real. |

## Nova Instalação - Tutorial Completo

### 1. Instale os pré-requisitos

Instale os seguintes softwares no Windows:

- [WibWobPadaBoom](https://mega.nz/file/Ctx3zQwT#4uBpoPU1ptBAHDWYnFcBMhjngXK_WWwYFVl79GIUqME) o projeto principal (descompacte-o);
- [.NET SDK 8](https://dotnet.microsoft.com/download/dotnet/8.0) para o servidor;
- [PostgreSQL](https://www.postgresql.org/download/) 18 para contas e backups;
- [Apktool](./JavaTools.zip);
- [Java JDK 21](https://www.oracle.com/fr/java/technologies/downloads/#jdk21-windows);
- Android SDK Build-Tools para gerar o APK.

Não é necessário ter o Python instalado para o usar os executáveis fornecidos.

Abra o PowerShell e verifique as instalações:

```powershell
dotnet --version
& 'C:\Program Files\PostgreSQL\18\bin\psql.exe' --version
java -version
apktool --version
```

Se você estiver usando uma versão diferente do PostgreSQL, adapte o número `18` nos caminhos indicados abaixo.

### 2. Configure o servidor

1. Descompacte o projeto em uma pasta onde você tenha permissões escritas.
2. Copie `appsettings.example.json`.
3. Renomeie a cópia para `appsettings.Development.json`.
4. Execute o comando `ipconfig` e anote o endereço IPv4 do computador, por exemplo, `192.168.1.100`.
5. Abra o arquivo `appsettings.Development.json` e e insira as seguintes informações:

   ```json
   {
     "PostgresConnectionString": "Host=127.0.0.1;Port=5432;Database=wibwob;Username=postgres;Password=PASSWORD",
     "PublicServerURL": "http://192.168.1.100:5000"
   }
   ```

Substitua o endereço IP e a senha pelos seus própros valores. Para um telefone, não use `localhost`.

### 3. Criar e importar o banco de dados

A partir do PowerShell, localize no diretório raiz do projeto:

```powershell
& 'C:\Program Files\PostgreSQL\18\bin\createdb.exe' -U postgres wibwob
& 'C:\Program Files\PostgreSQL\18\bin\psql.exe' -U postgres -d wibwob -f .\WWR_BACKUP\backup_nomail.sql
& 'C:\Program Files\PostgreSQL\18\bin\psql.exe' -U postgres -d wibwob -c 'CREATE TABLE IF NOT EXISTS public.mail (mail text PRIMARY KEY, "currentUdkey" text);'
```

A importação pode demorar vários minutos. Execute-a apenas uma vez e não importe também o arquivo `Database/schema.sql`.

### 4. Inicar e verificar o servidor

1. Clique duas vezes no arquivo `LANCER_WIBWOB.bat`.
2. Mantenha a janela do servidor aberta.
3. No PC, abra `http://127.0.0.1:50/eal/help.html`.
4. No celular conectado à mesma rede Wi-Fi, abra `http://IP_DO_SEU_PC:5000/eal/help.html`.

Se o teste funcionar no PC, mas não no celular, permitar as portas do servidor no firewall do Windows e verifique se ambos os dispositivos estão usando a mesma rede.

### 5. Criar o APK

1. Execute o arquivo `CUSTOM_APK_BUILDER/WibWobApkBuilder.exe`.
2. Escolha **Francês** ou **Inglês** para a interface do criador.
3. Selecione o APK em inglês que você obteve legalmente.
4. Insira o endereço IPv4 e a porta `5000` do seu computador.
5. Especifique as pastas Java, Android Build-Tools e `apktool.bat` caso a detecção automática falhe.
6. Clique em **Criar APK**
7. Instale o APK gerado no seu dispositivo Android.

O guia detalhado está disponível em [TEST_APK_LOCAL.pt-BR.md](TEST_APK_LOCAL.pt-BR.md)

## Atualizando de uma versão anterior

> [!IMPORTANT]
> Não reimporte o arquivo `backup_nomail.sql` se o seu banco de dados `wibwbob` já tiver suas contas.

1. Desligue completamente o servidor usando `Ctrl+C`.
2. Faça backup dos seguintes itens :
   - `appsettings.Development.json` ;
   - seu banco de dados PostgreSQL `wibwob` ;
   - `ADMIN_CLIENT/backups/`, se esta pasta existir ;
   - sua chave `CUSTOM_APK_BUILDER/wibwob-custom-test.keystore`.
3. Copie o conteúdo do pacote de atualização para a pasta do projeto antigo e aceita a substituição de arquivos.
4. Mantenha seu arquivo `appsettings.Development.json` antigo: não o substitua pelo arquivo de exemplo.
5. Mantenha seu banco de dados PostgreSQL existente: não renicie o `createdb` nem a importação SQL.
6. Verifique se estes arquivos estão presentes :
   - `ADMIN_CLIENT/WibWobAdmin.exe` ;
   - `CUSTOM_APK_BUILDER/lang/fr.lang` ;
   - `CUSTOM_APK_BUILDER/lang/en.lang` ;
7. Execute novamente `LANCER_WIBWOB.bat`.
8. Recrie o seu APK somente se o seu endereço IP do servidor tiver mudado ou se o seu APK antigo não conectar mais.

Os executáveis antigos `WibWobAdmin.exe` e `WibWobApkBuilder.exe` não são mais usados. Execute apenas as versões com o sufixo ``.

## Administração

Execute `ADMIN_CLIENT/WibWobAdmin.exe`. O servidor deve ser interrompido antes de qualquer modificação direita no banco de dados, pois seu cache pode sobrescrever dados antigos.

O cliente de administração cria um backup antes de gravações confidenciais. Nunca publique backups de contas.

## Segurança

- Nunca torne o PostgreSQL acessível pela internet.
- Não publique o arquivo `appsettings.Development.json`, uma chave de assinatura ou um backup de conta.
- Abra apenas as portas HTTP essenciais em uma rede confiável.
- Use um APK obtido legalmente.

## Documentação

- [Instalação do Servidor e PostgreSQL](START_WIBWOB.md)
- [Criação e Instalação do APK](TEST_APK_LOCAL.pt-BR.md)
- [Usando o Cliente Administrador](ADMIN_CLIENT/README.pt-BR)

## Créditos

Projetos baseado em **Puniemu**.

- Zura e DarkCraft - Desenvolvimento Principal
- wibwob_yt - Desenvolvimento
- onepiecefreak3 e kuronosuFear - Assistência em Engenharia Reversa
- picky_x_keizen - Logotipo

Configuração e ferramentas locais : **TheC0mmand**.
