# WibWob Reload ( um vídeo tutorial será lançado em breve )

**Você pode atulizar se tiver uma versão mais antiga do projeto**
[Atualizar](#Atualizar-de-uma-versão-antiga)

**Documentação : Português do Brasil [Français](README.md) | [English](README.en.md)**

Servidor local e experimental para a comunidade para **Yo-kai Watch Wibble Wobble**

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
| `WWR_BACKUP/` |Faz um backup do PostgreSQL e dos recursos necessários para o servidor. |
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
2. Abra o arquivo `appsettings.Development.json`.
3. Execute o comando `ipconfig` e anote o endereço IPv4 do computador, por exemplo, `192.168.1.100`.
4. Abra o arquivo `appsettings.Development.json` e e insira as seguintes informações:

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



