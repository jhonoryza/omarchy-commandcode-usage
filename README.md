# Command Code Usage for Omarchy agents panel

Menampilkan usage `command-code` / `cmd` di panel `omarchy.agents`, meniru pola
[`wellatleastitried/omarchy-copilot-panel-usage`](https://github.com/wellatleastitried/omarchy-copilot-panel-usage).

## Cara kerja

* `bin/omarchy-agent-usage-commandcode` scan `~/.commandcode/projects/*/*.jsonl`
  (skip `*.checkpoints.jsonl`, `*.prompts.jsonl`), hitung prompt/token per hari
  dan per model, tulis ke `~/.local/state/omarchy/agents/usage/commandcode.json`.
* `ui/main.qml` jalan tiap 5 menit + saat usage dir berubah, sama seperti plugin Copilot.
* Panel `omarchy.agents` otomatis menampilkan tab baru begitu file JSON-nya ada —
  tanpa edit `/usr/share/omarchy`.

## Test manual

```bash
~/.config/omarchy/plugins/dell.commandcode-usage/bin/omarchy-agent-usage-commandcode | head -n 40
~/.config/omarchy/plugins/dell.commandcode-usage/bin/omarchy-agent-usage-commandcode --write
cat ~/.local/state/omarchy/agents/usage/commandcode.json | head -n 40
omarchy plugin validate ~/.config/omarchy/plugins/dell.commandcode-usage
omarchy-shell shell rescanPlugins
```

## Catatan

* `command-code` tidak punya endpoint quota publik, jadi `limits: []` —
  yang tampil: today, 7 hari terakhir, total per model.
* Kalau mau icon sendiri, tambah `assets/commandcode.svg` (+ `commandcode-light.svg`
  untuk light theme). Tanpa itu panel pakai glyph default.
