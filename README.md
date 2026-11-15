# Suricata Sentinel Live — avatar definitions

Suricata is a citizen movement for checking claims before sharing them. **Sentinel Live** will lay a fact-check overlay over any video you watch; in its version 2, the checks are presented by AI avatars.

This repository is the **public, single source of truth** for those avatars: who they are, what they cover, which kinds of sources they may use, their evidence rules and their tone. One JSON file per avatar in [`avatars/`](avatars/).

> **Status: concept.** No avatar is live yet. Looks and voices don't exist yet, and every source is marked *(planned)* until a real connection exists. Every avatar is always labelled as AI.

## Who decides what

| Who | Can do |
| --- | --- |
| **Viewers** | Switch any avatar on or off for themselves (website, extension, second screen). That's all. |
| **Community** | Read every definition here and **propose** changes: open an issue with the [*Avatar change proposal*](../../issues/new/choose) form, or a pull request. |
| **Suricata team** | Reviews and merges. Only the team can change a definition ([`CODEOWNERS`](.github/CODEOWNERS)). |

**Switching avatars off never hides a check.** It changes *who presents* it: the matching expert → the host (Skopos) → text only. A viewer can't filter out verdicts they don't like by turning an avatar off.

## The line-up (12)

**Hosts and roles** — mythological names, the same in every language:

| id | Name | Job | On by default |
| --- | --- | --- | --- |
| `skopos` | Skopos | Host: opens, routes, presents opinions and checks of switched-off experts, sums up | yes |
| `heimdall` | Heimdall | First alert: "a claim was made, checking…", says when something can't be checked yet | no (speaks often) |
| `maat` | Maat | Explains how a verdict was reached when evidence is mixed; announces corrections | yes |

**Experts** — ordinary first names, localized per language (`names.<lang>`, falling back to `names.default`):

| id | pl / cs / default | Subject |
| --- | --- | --- |
| `science-health` | Zofia / Žofie / Sophie | Science & health |
| `statistics-economy` | Tomasz / Tomáš / Thomas | Statistics & economy |
| `law` | Helena / Helena / Helen | Law & constitution |
| `politics-elections` | Marek / Marek / Mark | Politics & elections |
| `climate-energy` | Ewa / Eva / Eve | Climate, environment & energy |
| `international` | Adam / Adam / Adam | World & conflicts |
| `media-images` | Maja / Maja / Maya | Media, images & deepfakes |
| `history` | Piotr / Petr / Peter | History |
| `technology` | Natalia / Natálie / Natalie | Technology & AI |

## File format

Validated by [`schema/avatar.schema.json`](schema/avatar.schema.json). Every push and pull request is checked automatically (*Validate avatars* workflow). The file name must match the `id`.

- `kind`: `role` (global name, `nameOrigin`, `handles`) or `expert` (localized names, `domains`, `sources`, `evidencePolicy`).
- `status`: `concept` → `testing` → `live` → `retired`. Bump `version` on every change.
- `title`, `job`: viewer-facing text, at least `en` and `pl`; add any BCP 47 language.
- `models`: ordered list, the first is used and the rest are fallbacks.
- `sources`: localized source *types* (`en`, `pl`, …) marked "(planned)" until a real connector exists. Never list a source we don't actually use.
- `look`, `voice`: `null` until designed.

## Review rules for changes

1. **Neutrality.** One standard for every party, country and group. No avatar may favour a side.
2. **Sources.** New sources need: who publishes them, why they're reliable, and how corrections are handled.
3. **Names and looks.** Original personas only — never resembling a real person. A new language name needs a native-speaker check. Mythological names get a cultural check.
4. **Always labelled AI** (EU AI Act Art. 50).
5. Every merged change gets a line in [`CHANGELOG.md`](CHANGELOG.md) with the reason.

## How to propose a change

1. Read the avatar's file in [`avatars/`](avatars/).
2. Open an [*Avatar change proposal*](../../issues/new/choose): say what should change and why, with examples.
3. Or fork, edit the JSON (bump `version`) and open a pull request. The automatic check must pass.
4. The Suricata team reviews it against the rules above, and merges, asks for changes or explains a refusal.

## License and brand

- **Avatar definitions and documentation:** [CC BY 4.0](LICENSE). Free to use, adapt and share, including commercially, if you credit us and mark your changes.
- **Schema and workflows** (`schema/`, `.github/`): [MIT](LICENSE-CODE).
- **Names and logo are not licensed.** You may credit Suricata as the source, but you may not use our name for your product or imply that we endorse it. See [TRADEMARKS.md](TRADEMARKS.md).
