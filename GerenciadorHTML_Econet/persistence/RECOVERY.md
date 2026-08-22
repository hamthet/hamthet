# Protocolo de recuperação DEV

1. Ler `LATEST.json` na branch `gerenciadorhtml-econet-dev`.
2. Ler o manifesto indicado por `manifest_path`.
3. Obter a baseline `GerenciadorHTML_Econet_2108_V3.zip` do armazenamento de arquivos da conversa/biblioteca; não confiar apenas no filesystem efêmero.
4. Validar SHA-256 da baseline antes de qualquer alteração.
5. Recuperar todos os chunks listados no manifesto do GitHub e concatená-los na ordem declarada.
6. A chave AES-256-GCM é um segredo operacional e NÃO está neste repositório público; ela é fornecida privadamente à automação.
7. Descriptografar o payload, validar `delta_payload_sha256`, extrair e aplicar os patches com os strip levels declarados no manifesto.
8. Executar os harnesses/auditorias do checkpoint recuperado antes de novos patches.
9. Se qualquer hash, arquivo, chunk, decrypt ou auditoria falhar, abortar a alteração (fail-closed).
10. Após um patch internamente validado, persistir um novo checkpoint cifrado no GitHub e só depois atualizar `LATEST.json`.

Nunca armazenar código-fonte Econet em claro neste repositório, pois o repositório hospedeiro é público. Estado persistido aqui é exclusivamente DEV; V4.2 continua sendo a última base aprovada.
