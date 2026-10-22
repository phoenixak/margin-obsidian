# Margin AI Proofreader

An AI second pass for [Harper](https://writewithharper.com) in Obsidian: purple underlines for what Harper's rules can't catch (agreement, tense, wrong-but-real words, run-ons), with a hover card to Apply or Ignore, and **Rewrite selection…** (command palette or right-click). It never repeats what Harper flags. Not affiliated with Harper or Automattic.

## Install

From Obsidian: Settings → Community plugins → Browse → search "Margin AI Proofreader". Also install **Harper**.

Manual: download `main.js`, `manifest.json` and `styles.css` from the latest release into `<vault>/.obsidian/plugins/margin-ai-proofreader/`.

## Where your text goes

- **Local model** (Ollama / LM Studio): text stays on this device. Obsidian's own network API is used, so **no OLLAMA_ORIGINS or CORS setup is needed**. Use **Find models** in Margin's settings. Tested with Ollama and `gemma4:26b-a4b-it-qat` alongside Harper's plugin: on 12 real READMEs and docs it added 15 underlines next to Harper's 425, none on the same spot.
- **Gemini API**: sent to Google with your key; on the free tier Google may use it to improve its products. The key is kept in Obsidian's secret storage (device-local, not synced, never in `data.json`); needs Obsidian 1.11.4+.
- Nothing is sent until you choose. Folders listed under "Never check these folders" are never sent.

## Works with Harper's plugin

Margin asks Harper's own Obsidian plugin what it already flags and skips those, so install and enable **Harper** too. (Margin doesn't bundle a second copy of Harper; that keeps it about 1 MB.)

## Honest status

Tested in Obsidian 1.14.4 on Windows (desktop): underlines, hover card, Apply and rewrite, with the local-provider code path against a mock server. Dedup was verified against a stand-in for Harper's plugin (same `lint()` interface), not yet with Harper's plugin itself. Desktop only for now.

## Source

This repository is generated from [phoenixak/margin](https://github.com/phoenixak/margin) (`packages/obsidian` and `packages/core`), which also has the VS Code extension, browser extension and language server. Please open issues and pull requests there.

Build: Node 22+, then `npm ci && npm run build`; the plugin files are in `dist/`. Releases are built by GitHub Actions with signed build provenance.
