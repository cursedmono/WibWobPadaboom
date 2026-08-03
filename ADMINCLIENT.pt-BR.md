# Cliente de Administração do Wib Wob Reload

**Documentação: Português do Brasil | [Français](ADMINCLIENT.md) | [English](ADMINCLIENT.en.md)**

O Cliente de Administração gerencia contas armazenadas no servidor PostgreSQL local.

>[!WARNING]
>O projeto oferece suporte à **versão do jogo em inglês**. O Admin Client não traduz os dados do jogo.

## Primeiros Passos

1. Configure e importe o PostgreSQL conforme descrito em `README.pt-BR.md`.
2. Interrompa o servidor antes de modificar o bando de dados diretamente.
3. Execute o `WibWobAdmin.exe`.

Não é necessário ter o Python instalado para usar o executável da versão lançada.

## Principais Recursos

- Iniciar e parar o servidor local;
- Pesquisar e inspecionar contas;
- editar recursos do jogador e recursos do jogador;
- conceder itens;
- editar o nível, HP e ataque de um Yo-kai que você possui;
- desbloquear progressão;
- transferir dados de salvamento entre duas contas;
- reparar ou restaurar o banco de dados.

## Backups de Segurança

- Um backup é criado antes de operações sensíveis.
- Nunca publique o contéudo da pasta `backups`
- Nunca compartilhe uma GDKey, senha do PostgreSQL ou arquivo `appsettings.Development.json`.
- O botão de parada só pode interromper um servidor iniciado pelo Admin Client.

## Importante

O servidor em execução mantém contas carregadas na memória. Portanto, uma edição direta no PostgreSQL pode ser sobresctrita pelo cache do sercvidor. sempre pare o servidor antes de salvar uma modificação.
