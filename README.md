# FreeMyProjector LDZ

Tela inicial leve para projetores Android, com navegação pelo controle remoto, favoritos e acesso aos ajustes de projeção e ao menu original.

Testado em HY300 Magic Cube com firmware TXCZ e Android 12. Outros firmwares precisam de validação.

**Publicação inicial:** a versão definitiva e seu APK ainda estão em preparação. Nenhum APK final está disponível neste repositório.

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

Quando o APK definitivo estiver publicado, baixe-o em **Releases** e ajuste o caminho no comando:

```powershell
.\adb.exe -s $alvo install -r 'CAMINHO_DO_APK.apk'
.\adb.exe -s $alvo shell am start -n br.com.ldz.freemyprojector/.ProjectorHomeActivity
```

O parâmetro `-r` atualiza uma instalação com assinatura compatível. A instalação e a abertura direta foram testadas; definir a home padrão é uma etapa separada. Preserve o launcher original para poder retornar a ele.

## Créditos

Derivado de [Free My TV](https://github.com/simbasjungles/free-my-tv), sob licença MIT, com adaptações do FreeMyTV LDZ. Fork não oficial; os avisos e termos originais estão em [LICENSE](LICENSE).
