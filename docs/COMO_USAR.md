# Como usar

## Instalar

1. Copie `DiviTrix-1.0.1-release.apk` para o celular (cabo, Drive, Telegram etc.).
2. Abra o arquivo e permita **"Instalar apps desconhecidos"** para o app usado
   na abertura (Arquivos, Chrome etc.).
3. Confirme a instalação.

Via ADB:

```bash
adb install "dist/DiviTrix-1.0.1-release.apk"
```

O app não pede nenhuma permissão de câmera, microfone, contatos ou
armazenamento.

## Dividir um vídeo

1. Abra o **DiviTrix**.
2. Toque em **Escolher vídeo**.
3. Selecione o vídeo no seletor do Android.
4. Confira a **pré-visualização** e toque no vídeo para dar play e confirmar que é o arquivo correto.
5. Toque em **Dividir em partes de 30s** e aguarde a barra de progresso. Você pode cancelar a qualquer momento.

O tempo varia com o tamanho do vídeo, mas costuma ser bem rápido porque nada é
reencodado — é só cópia de dados.

## Compartilhar no WhatsApp

Na tela de resultado você tem duas opções:

| Botão | O que faz |
|---|---|
| **Compartilhar no WhatsApp** | Abre o WhatsApp com **todas as partes** anexadas de uma vez. |
| **Compartilhar em outro app** | Abre o seletor do Android (Drive, Telegram, e-mail etc.). |

### Por que às vezes o WhatsApp comprime?

Quando você envia um vídeo como **mídia**, o WhatsApp reencoda para reduzir o
tamanho. Se precisar do arquivo idêntico ao original, use **Compartilhar em
outro app** e escolha Drive, e-mail ou outro destino que envie o MP4 sem
recompressão.

### Limite de arquivos

O WhatsApp pode limitar quantos vídeos aceita por envio (varia por versão). Se
ele recusar o grupo inteiro:

- envie em grupos menores;
- ou compartilhe por outro app.

## Onde ficam os arquivos

```
Android/data/com.cleber.divitrix/files/Movies/Divitrix/<data_hora>/
```

Essa pasta é privada do app; os arquivos **não aparecem na galeria**. Ao iniciar
ao escolher outro vídeo, as partes anteriores são apagadas automaticamente para não
acumular vídeos.

Para guardar uma parte permanentemente, compartilhe com o Drive/Arquivos ou
mova o arquivo pelo gerenciador de arquivos.

## Perguntas frequentes

**O vídeo ficou com 31s, não 30s. É normal?**
Sim. O corte é feito no keyframe mais próximo depois dos 30s para não reencodar.
Dependendo do GOP, a parte fica entre 30 e 32s (ou mais, se o GOP for longo).

**A qualidade mudou?**
Não. Os samples comprimidos são copiados; não há decoder/encoder no caminho.

**Por que o app não abre vídeos do WhatsApp?**
Vídeos recebidos podem estar em formatos/containers não suportados pelo
`MediaMuxer` do aparelho. Converta para MP4/H.264 ou teste em outro aparelho.

**Apareceu "Espaço insuficiente".**
A divisão cria uma cópia completa do vídeo. Libere espaço equivalente ao
tamanho do arquivo original (mais uma margem de 100 MB).

**O compartilhamento não abre o WhatsApp.**
Verifique se o WhatsApp está instalado. Se estiver, o app cai no seletor padrão
do Android; escolha o WhatsApp manualmente.

**Posso dividir vídeos com mais de 1 hora?**
Sim, mas o resultado terá muitas partes (uma a cada ~30s) e ocupará o mesmo
espaço do original. O limite interno é de 5.000 partes.

**Perdi o keystore. E agora?**
Sem o keystore original não é possível atualizar o app já instalado; será
preciso desinstalar e instalar uma nova assinatura. Guarde
`keystore/divitrix-release.jks` e `keystore.properties` em local seguro.
