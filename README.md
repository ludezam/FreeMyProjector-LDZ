# FreeMyProjector LDZ

Tela inicial leve para projetores Android, com navegação pelo controle remoto, favoritos e acesso aos ajustes de projeção e ao menu original.

Testado em HY300 Magic Cube com firmware TXCZ e Android 12. Outros firmwares precisam de validação.

**Versão 1.2.0:** [baixar APK](https://github.com/ludezam/FreeMyProjector-LDZ/releases/download/v1.2.0/FreeMyProjector-LDZ-1.2.0.apk) · [Releases](https://github.com/ludezam/FreeMyProjector-LDZ/releases)

Novidades: consulta e download de atualizações pelo GitHub, configuração automática na primeira abertura e navegação dos ajustes preservando a seleção ao voltar.

Favoritos editáveis, grade de aplicativos, ajustes próprios, preservação da home original e panorama instantâneo de memória. A otimização só desativa candidatos validados para o firmware; no HY300 testado, nenhum app foi desativado.

## Telas da versão 1.1.0

Capturas reais do projetor; os aplicativos exibidos dependem do que está instalado e não acompanham o APK.

| Home com paisagem e favoritos | Grade de aplicativos |
|---|---|
| ![Home](docs/screenshots/01-home.png) | ![Aplicativos](docs/screenshots/02-aplicativos.png) |
| **Ajustes com navegação pelo controle** | **Projeção e restauração da home** |
| ![Ajustes](docs/screenshots/03-ajustes.png) | ![Projeção](docs/screenshots/04-projecao.png) |
| **Mover ou desafixar favoritos** | **Panorama de memória antes e depois** |
| ![Favoritos](docs/screenshots/05-favoritos.png) | ![Memória](docs/screenshots/06-sobre.png) |

## Instalação pelo pendrive

Baixe o APK em Releases, copie para um pendrive e abra pelo gerenciador de arquivos do projetor. Autorize a instalação por essa origem se o Android solicitar. Depois, abra **FreeMyProjector LDZ**. A preparação e a ativação como home precisam do ADB local autorizado, conforme os passos abaixo.

## Instalação por ADB

### 1. Ativar a depuração

No projetor, abra **Activity Launcher → Configurações (`com.android.tv.set`) → `system.development.DevelopmentActivity` → Iniciar atividade**. Ative as opções do desenvolvedor, **Depuração USB** e **Internet Adb**. Esse foi o caminho confirmado no firmware testado.

### 2. Descobrir a porta

Instale o Termux no projetor pelo pendrive e execute:

```sh
getprop | grep adb
```

Consulte a porta em `service.adb.tcp.port` (ou `persist.adb.tcp.port`) e o serviço `init.svc.adbd`, que deve indicar `running`. Para consultar separadamente:

```sh
getprop service.adb.tcp.port
getprop persist.adb.tcp.port
getprop init.svc.adbd
```

Não presuma a porta 5555. A porta pode variar; consulte novamente se a conexão parar de funcionar. Uma propriedade vazia, sozinha, não confirma que o ADB esteja desligado.

### 3. Conectar pelo computador

Instale o [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools), conecte computador e projetor à mesma rede e consulte o IP nas configurações de rede do projetor.

No PowerShell, dentro da pasta do Platform-Tools, substitua os valores abaixo pelos dados do seu aparelho:

```powershell
$alvo = 'IP_DO_PROJETOR:PORTA_ADB'
.\adb.exe connect $alvo
.\adb.exe devices -l
```

Aceite a autorização no projetor, se solicitada. Continue quando o aparelho aparecer como `device`.

### 4. Instalar e abrir

Baixe o APK 1.2.0 em **Releases** e ajuste o caminho no comando:

```powershell
.\adb.exe -s $alvo install -r '.\FreeMyProjector-LDZ-1.2.0.apk'
.\adb.exe -s $alvo shell am start -n br.com.ldz.freemyprojector/.ProjectorHomeActivity
```

O parâmetro `-r` atualiza uma instalação com assinatura compatível, preservando os dados. Na primeira abertura de uma instalação nova, a configuração automática também ativa a home. Preserve o launcher original para poder retornar a ele.

## Primeira abertura e restauração

1. Mantenha a depuração ativa e aceite a autorização ADB do LDZ. A configuração começa automaticamente; se a conexão falhar, ajuste a porta em **Conexão ADB** e tente novamente.
2. O app preserva a identificação da home original e registra a memória inicial. O registro de recuperação fica em **Downloads/FreeMyProjector LDZ**; não é um backup completo do Android. Essa cópia automática requer Android 10 ou superior.
3. A configuração desativa apenas candidatos da lista validada para o fabricante, ativa a home LDZ e registra a memória posterior. No HY300 testado, nenhum app foi desativado. A home original permanece instalada. Atualizações preservam a configuração já concluída e os favoritos.
4. Para voltar, abra **Ajustes → Imagem e projeção → Restaurar home original**. **Desfazer otimizações** reativa os apps alterados pelo LDZ.

Na home, **+** adiciona favoritos e segurar **OK** permite mover ou desafixar. Use **Voltar** para sair dos menus. O panorama em **Sistema → Sobre o dispositivo** compara registros momentâneos, sem prometer ganho permanente ou medir velocidade.

## Atualizações

Em **Ajustes → Atualizações → Buscar atualizações**, o app consulta a última release estável deste repositório. Havendo uma versão mais recente, use **Baixar e instalar**. O download verifica tamanho, SHA-256, pacote, versão e a mesma assinatura da instalação atual. O Android pode pedir autorização para instalar por essa origem e confirmação da instalação.

A consulta acontece somente quando solicitada. Também é possível atualizar manualmente pelo APK em Releases, usando `install -r`. Quem está na 1.1.0 precisa instalar a 1.2.0 manualmente para passar a usar esse menu. A [API da última release](https://api.github.com/repos/ludezam/FreeMyProjector-LDZ/releases/latest) fornece os dados usados pelo app.

A consulta foi testada no HY300. A instalação pelo menu de uma release futura mais recente ainda não foi exercitada.

Pacote: `br.com.ldz.freemyprojector` · versão: `1.2.0` · versionCode: `8` · Android mínimo do APK: `8.0`; preparação automática com cópia pública: `10` ou superior.

## Créditos

Derivado de [Free My TV](https://github.com/simbasjungles/free-my-tv), sob licença MIT, com adaptações do FreeMyTV LDZ. Fork não oficial; os avisos e termos originais estão em [LICENSE](LICENSE).

## Projetos relacionados

- [FreeMyTV LDZ](https://github.com/ludezam/FreeMyTV-LDZ) — home personalizada para Google TV e Android TV.
- [Controle LDZ](https://github.com/ludezam/Controle-LDZ) — controle remoto local por Wi-Fi para Android TV e projetores Android.
