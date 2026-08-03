# Compilando e instalado o APK local

**Documentação : Português do Brasil | [Français](TEST_APK_LOCAL.md) | [English](TEST_APK_LOCAL.en.md)**

> [!WARNING]
> **O jogo permanece em inglês.** A escolha entre francês e inglês afeta apenas a interface do Builder e os logs.

> [!IMPORTANT]
> Utilize apenas um APK de origem que você tenha permissão legal para usar, Este projeto não fornece o APK comercial original.

## Requisitos

- Java JDK 21 com `JAVA_HOME` configurado;
- Android SDK Build-Tools com `ANDROID_SDK_ROOT` configurado;
- APKTool disponível no `PATH` ou selecionado na interface;
- Servidor e telefone conectados à mesma rede local.

Verifique as ferramentas:

```powershell
java -version
keytool -help
adb version
zipalign -h
apksigner --help
apktool --version
```

## Prepare a Rede

1. Obtenha o endereço IPv4 do PC usando o comando `ipconfig`.
2. Utilize esse endereço no campo `PublicServerURL`.
3. Inicie o servidor.
4. No celular, acesse `http://PC_IP:5000/eal/help.html`.

Não gere o APK antes que essa página esteja acessível.

## Utilize o APK Builder

1. Execute `CUSTOM_APK_BUILDER/WibWobAPkBuilder-Obfuscated.exe`.
2. Escolha **Français** ou **English**. A escolha será salva no arquivo `builder-settings.json`.
3. Selecione o APK de origem em inglês compatível.
4. Insira o endereço IPv4 do servidor e a porta pública (normalmente`5000`).
5. Selecione o Android Build-Tools, o Java e o `apktool` caso a detecção automática falhe.
6. Selecione o caminho de destino para o APK gerado.
7. Clique em **Build APK**.

A interface e as mensagens de log do próprio Builder são carregadas a partir de:

```text
CUSTOM_APK_BUILDER/lang/fr.lang
CUSTOM_APK_BUILDER/lang/en.lang
```

Mantenha a pasta `lang` ao lado do executável.

## Instalação no Android

Ative a depuração USB, conecte o telefone e execute:

```powershell
adb devices
adb install -r .\wwr_custom_server.apk
```

Se o Android informar uma assinatura diferente, desinstale o aplicativo anterior antes de tentar novamente. A desinstalação apaga os dados locais do aplicativo.

##Soluções de Problemas

| Problema | Verificação |
| --- | --- |
| Java não encotrado | Verifique a variável `JAVA_HOME` e renicie o Terminal. |
| Builds-Tools inválidas | Selecione a pasta que contém `zipalign.exe` e `apksigner.bat`. |
| APKTool não encontrado | Selecione diretamente o arquivo `apktool.bat`. |
| Host WibWob não encontrado | Confirme se o APK de origem é a versão em inglês suportada. |
| Erro de rede no jogo | Verifique o IP, as portas e o firewall, e reconstrua o APK. |
| Arquivo `.lang` ausente | Restaure a pasta `.lang` forncecida com o Builder. |
