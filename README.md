# Curso AntiPorn

Módulo do curso AntiPorn que ficava na aba "AntiPorn" do [FocusGuard](https://github.com/mycroft440/FocusGuard). Ele saiu do app e agora mora aqui.

## O que tem aqui

Os arquivos mantêm os mesmos caminhos que tinham no FocusGuard (`app/src/...`, pacote `com.focusguard`). Assim, dá para copiá-los de volta para um app Android sem ajustes.

| Caminho | Conteúdo |
| --- | --- |
| `app/src/main/java/com/focusguard/ui/compose/screens/RecoveryCourseGatewayScreen.kt` | Tela de entrada do curso |
| `app/src/main/java/com/focusguard/ui/compose/screens/RecoveryHubScreen.kt` | Jornada em 3 etapas (Entenda a armadilha, Desfaça a lavagem cerebral, Feche as portas), cartões dos livros e termo de proteção |
| `app/src/main/java/com/focusguard/ui/OfflineBookActivity.kt` | Leitor offline (WebView) dos livros |
| `app/src/main/java/com/focusguard/data/RecoveryJourney.kt` | Regras de progresso da jornada |
| `app/src/main/java/com/focusguard/data/RecoveryProtectionPreset.kt` | Pacote de proteção: pornografia sem data final e redes sociais por 180 dias |
| `app/src/main/assets/easypeasy/` | Livro EasyPeasy offline, com as traduções (~77 MB) |
| `app/src/main/assets/creator-instructions/` | E-book de instruções do criador |
| `app/src/main/res/layout/activity_offline_book.xml` | Layout do leitor |
| `app/src/main/res/values*/strings_recovery_course.xml` | Textos da tela de entrada, em todos os idiomas |
| `app/src/main/res/values*/strings_antiporn.xml` | Strings `recovery_*` e `nav_recovery` tiradas do `strings.xml` do FocusGuard |
| `app/src/test/...` | Testes unitários (`RecoveryJourneyTest`, `RecoveryProtectionPresetTest`, `OfflineBookAssetsTest`) |
| `integration/focusguard-integration.patch` | O código de ligação removido do FocusGuard: aba na navegação, rota no NavHost, `startRecoveryProtectionPreset` no `BlockingSessionManager`, exceção do curso no Modo Foco e registro da Activity no manifest |

## Como devolver o curso ao FocusGuard

Na raiz de um clone do FocusGuard:

```bash
cp -r ../cursoantiporn/app/. app/
git apply -R ../cursoantiporn/integration/focusguard-integration.patch
```

O patch foi gerado a partir do commit `c0ece5d` do FocusGuard. Se o código tiver mudado muito desde então, use `git apply -R --3way`.

Para o texto do Modo Foco voltar a citar a aba, troque `focus_mode_kiosk_description` de volta para "Use the side menu to access Protection, Pomodoro, and AntiPorn." (e a versão em `values-pt`).

## Dependências do app hospedeiro

O código chama estas classes do FocusGuard, que não estão neste repositório:

- `com.focusguard.ui.compose.theme.*`: cores e cartões do tema
- `BlockingSessionManager`, `ProtectionPermissionGate`, `PermissionsActivity`, `FocusGuardLogger`
- `PredefinedWebsites.PORNOGRAPHY_RULE` e `BlockTargetPolicy`, usados pelo pacote de proteção
- A string compartilhada `status_close` e a cor `dark_bg`
