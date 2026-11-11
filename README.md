# Vetee API pro Codex

Codex plugin se skilly a OAuth MCP připojeními pro práci s Vetee GraphQL API.
**Výchozí režim je pouze čtení — GraphQL query a introspekce. Mutace jsou přísně
zakázané, dokud uživatel výslovně nepožádá o konkrétní změnu.** Přihlášení,
spuštění skillu ani nalezený problém nejsou souhlas se zápisem.

**Výchozí prostředí je master (produkce).** Beta a stage se používají při výslovném
výběru prostředí nebo jejich skillu. Veřejný balíček obsahuje jen instrukce a
konfiguraci připojení; přístup k datům vyžaduje přihlášení a příslušná oprávnění.

## Instalace

V aktuálním Codex CLI přidejte marketplace a plugin:

```sh
codex plugin marketplace add https://github.com/vetee-ai/vetee-codex-plugin.git
codex plugin add vetee-api@vetee
```

Pro lokální instalaci z klonu spusťte v kořeni tohoto repozitáře:

```sh
codex plugin marketplace add .
codex plugin add vetee-api@vetee
```

Potom otevřete novou konverzaci. V desktopovém Codexu lze plugin instalovat také
z marketplace **Vetee** v adresáři pluginů. Pokud CLI nezná příkaz `plugin`,
aktualizujte Codex. Balíček používá podporovaný Codex formát
`plugins/vetee-api/.codex-plugin/plugin.json` a odpovídající `.mcp.json`,
včetně nastavení OAuth callbacku. Marketplace je v `.agents/plugins/marketplace.json`.

## Prostředí a použití

| Prostředí | Skill | MCP připojení | Endpoint |
| --- | --- | --- | --- |
| master — výchozí, produkce | `$vetee-api` | `vetee-api` | `https://api-mcp.vetee.pet/mcp` |
| beta | `$vetee-beta-api` | `vetee-beta-api` | `https://api-mcp.beta.vetee.pet/mcp` |
| stage | `$vetee-stage-api` | `vetee-stage-api` | `https://api-mcp.stage.vetee.pet/mcp` |

Například:

```text
$vetee-api Zjisti dostupné možnosti filtrování vybraného seznamu.
$vetee-beta-api Ověř strukturu vstupu pro požadovanou mutaci.
$vetee-stage-api Proveď požadovanou změnu a ověř výsledek.
```

Codex může skilly zobrazovat s prefixem pluginu, například
`vetee-api:vetee-api`, `vetee-api:vetee-beta-api` a `vetee-api:vetee-stage-api`.
V takovém případě vyberte příslušnou položku v nabídce skillů.

Bez určeného prostředí se používá master. Přihlášení ani chyba na jednom prostředí
nezpůsobí přepnutí na jiné. Nástroj `admin_query` slouží pro čtení a introspekci;
`admin_mutation` se smí použít jen pro konkrétní změny výslovně požadované uživatelem. Podrobný postup je v
[GraphQL workflow](plugins/vetee-api/references/graphql.md). Schéma se načítá z vybraného prostředí.

## API reference

Skilly odkazují podle potřeby na samostatné reference odvozené z dokumentace Vetee:

- [Základy GraphQL](plugins/vetee-api/references/graphql-basics.md)
- [Nastavení aplikace](plugins/vetee-api/references/app-settings.md)
- [Nahrání souboru](plugins/vetee-api/references/upload-file.md)
- [Otevření souboru](plugins/vetee-api/references/open-file.md)

Administrativní domény popisují modely a operace dostupné přes API:

- [Stories](plugins/vetee-api/references/stories.md)
- [Nabídky, objednávky a platby](plugins/vetee-api/references/offers-orders-and-payments.md)
- [Konzultace](plugins/vetee-api/references/consultations.md)
- [Referenční data](plugins/vetee-api/references/reference-data.md)
- [Zvířata](plugins/vetee-api/references/animals.md)
- [Zařízení a ordinace](plugins/vetee-api/references/facilities.md)
- [Obsah a články](plugins/vetee-api/references/content-and-articles.md)
- [Shop](plugins/vetee-api/references/shop.md)

Každá doména má vlastní dokument a odkazy na jednotlivé podstránky ve stejnojmenné
podsložce. Reference popisují význam modelů, překlady, filtry a správu dat;
uživatelské postupy aplikace jsou vynechané. Popis mutace není povolením k jejímu
spuštění. Skutečné schéma a dostupnost operací se ověřují ve vybraném prostředí.

Nahrávání a zobrazení souborů jsou popsané jako HTTP operace; dokumentace
nepřidává nové MCP nástroje. Přístupové odkazy na zdrojové dokumenty a jejich
guest tokeny nejsou součástí veřejného balíčku.

## OAuth a zapamatování přihlášení

Každé připojení používá veřejného OAuth klienta `api-mcp` s PKCE a vlastním
callbackem na lokálním portu `1456`. `client_id` je veřejný identifikátor,
žádný client secret se do balíčku nepřidává. Port musí být při přihlašování volný;
jednotlivá prostředí přihlašujte postupně.

Po instalaci pluginu nejdřív vypište dostupná MCP připojení:

```sh
codex mcp list
```

Přihlášení do výchozího prostředí **master**:

```sh
codex mcp login vetee-api
```

Přihlášení do **beta**:

```sh
codex mcp login vetee-beta-api
```

Přihlášení do **stage**:

```sh
codex mcp login vetee-stage-api
```

Každý příkaz spustí OAuth přihlášení v prohlížeči. Stačí přihlásit prostředí,
které chcete používat; příkazy spouštějte postupně. Pokud `codex mcp list`
zobrazuje název s prefixem pluginu, použijte v login příkazu přesně celý název
z tohoto výpisu místo krátkého názvu uvedeného výše.

Po přihlášení zkontrolujte připojení znovu:

```sh
codex mcp list
```

V desktopovém Codexu lze stejné přihlášení spustit přes OAuth nabídku vybraného
MCP připojení.

**Tokeny ukládá a obnovuje Codex.** Plugin je neukládá do repozitáře, `.env`,
konverzace ani vlastního cache. Stejné názvy serverů, URL a OAuth klienta zachovávají
identitu připojení mezi spuštěními. Nové přihlášení není potřeba pro každou úlohu.

Pro výslovné uložení do systémové klíčenky nastavte v uživatelském
`~/.codex/config.toml` na nejvyšší úrovni, před sekcemi `[... ]`:

```toml
mcp_oauth_credentials_store = "keyring"
```

Toto je uživatelské nastavení Codexu, nikoli konfigurace pluginu. Režim `keyring`
vyžaduje dostupnou systémovou klíčenku; výchozí `auto` vybírá dostupné úložiště.
Používejte stejný OS účet a stejný Codex profil při loginu i dalších spuštěních.
Po přihlášení otevřete novou konverzaci nebo restartujte Codex a zkuste krátký
read-only dotaz. Pokud se žádá přihlášení znovu, zkontrolujte dostupnost klíčenky,
stejný profil a název připojení. Nevytvářejte druhé ruční MCP připojení se stejnou
URL jako náhradu za plugin a nepřekopírovávejte tokeny mezi připojeními.

## Aktualizace

```sh
codex plugin marketplace upgrade vetee
codex plugin add vetee-api@vetee
```

Po aktualizaci otevřete novou konverzaci. Aktualizace instrukcí nemění OAuth
identitu připojení; vypršení nebo odvolání přístupu může vyžadovat nový login.

## Formát a dokumentace

- [Codex plugin packaging](https://developers.openai.com/plugins/build/plugins)
- [MCP a OAuth v Codexu](https://developers.openai.com/codex/mcp/)
- [Konfigurace úložiště OAuth](https://developers.openai.com/codex/config-reference/)
