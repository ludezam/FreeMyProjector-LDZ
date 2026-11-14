FreeMyProjector LDZ 1.2.0 — atualização pelo GitHub, configuração automática e navegação.

- Buscar atualizações consulta a última release estável deste repositório somente quando solicitado.
- Baixar e instalar verifica origem, tamanho, SHA-256, pacote, versionCode e assinatura. O Android mantém a autorização e a confirmação da instalação.
- Primeira configuração automática: preserva a home original e a recuperação em Downloads, registra a memória, aplica somente otimizações validadas e ativa a home LDZ. No HY300 testado, nenhum app foi desativado.
- Atualizações preservam favoritos e a configuração concluída.
- Voltar nos ajustes preserva histórico, seleção e posição da lista, inclusive após abrir painéis nativos.

Para atualizar a 1.1.0, instale manualmente `FreeMyProjector-LDZ-1.2.0.apk` sem desinstalar a versão anterior. Exemplo: `adb install -r FreeMyProjector-LDZ-1.2.0.apk`. A partir da 1.2.0, use o menu Atualizações para consultar futuras releases.

Pacote `br.com.ldz.freemyprojector`, versionCode `8`. Android mínimo do APK: 8.0; preparação automática com cópia pública: Android 10 ou superior. Validado no HY300/TXCZ com Android 12; outros firmwares precisam de validação.

Consulta real ao GitHub, revalidação automática e navegação testadas. Download e instalação pelo menu de uma release futura mais recente ainda não foram exercitados. A revalidação foi testada sem apagar os dados existentes.

APK assinado com o mesmo certificado da 1.1.0. Confira `SHA256SUMS.txt` para validar o download.
