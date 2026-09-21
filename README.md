# PNG IPTC Tagger

Strumento browser-based per scrivere metadati IPTC (e XMP) direttamente nei file PNG, senza convertirli in un altro formato. Pensato per i PNG scontornati (con trasparenza) usati nei materiali Panini.

**Zero installazione.** Apri la pagina, trascina i file, scarica il risultato. Tutto avviene nel tuo browser: nessun file viene caricato su un server esterno.

🔗 **Apri lo strumento:** _(link alla pagina GitHub Pages, es. `ttps://sebamc2023.github.io/PICTURES-png-iptc-tagger/`)_

---

## Come si usa

1. **Carica i PNG** — trascina uno o più file nell'area di caricamento, oppure clicca per selezionarli dal tuo computer.
2. **Compila i campi IPTC:**
   - **Title** — titolo dell'immagine
   - **Description** — descrizione/didascalia
   - **Description Writer** — chi ha scritto/revisionato la didascalia
   - **Keywords** — parole chiave, separate da virgola
   - **Instructions** — istruzioni d'uso interne
3. **(Opzionale) Usa i segnaposto** per compilare i campi automaticamente in base al nome file, alla cartella o a un numero progressivo — stessa sintassi dei segnaposto di ACDSee. Segnaposto disponibili:
   - `<File Properties:Filename>` — nome file completo
   - `<File Properties:Filename (w/o extension)>` — nome file senza estensione
   - `<File Properties:Extension>` — estensione
   - `<File Properties:Folder>` — cartella di provenienza (se disponibile)
   - `<Counter>`, `<Counter:2>`, `<Counter:3>` — numero progressivo nel lotto (1, 01, 001…)
   - `<Content:Title>`, `<Content:Description>` — richiamano il valore già digitato negli altri campi
4. **Premi "Scrivi IPTC e scarica".** Con un solo file scarichi il PNG taggato; con più file scarichi uno ZIP con tutti i file taggati.

I file originali non vengono mai modificati: lo strumento produce sempre delle copie.

## Compatibilità

I metadati vengono scritti in due formati in parallelo, per la massima compatibilità:

| Campo tool | Tag IPTC (legacy) | Tag XMP |
|---|---|---|
| Title | Object Name | `dc:title` |
| Description | Caption-Abstract | `dc:description` |
| Description Writer | Writer/Editor | `photoshop:CaptionWriter` |
| Keywords | Keywords | `dc:subject` |
| Instructions | Special Instructions | `photoshop:Instructions` |

I dati sono leggibili con ExifTool, Adobe Bridge, Photoshop, ACDSee e la maggior parte dei DAM. Se ritagghi un file già elaborato da questo strumento, i metadati precedenti vengono sostituiti (non duplicati).

## Note tecniche

Il PNG non ha un chunk nativo per l'IPTC-IIM classico. Lo strumento aggira il problema seguendo la stessa convenzione usata da ExifTool e ImageMagick: i dati IPTC vengono incapsulati in un blocco Photoshop (8BIM) all'interno di un chunk PNG `zTXt` con etichetta `Raw profile type iptc`, mentre l'XMP viene scritto in un chunk `iTXt` standard. Nessuna conversione di formato, nessuna dipendenza esterna installata: tutto il lavoro sui chunk PNG è fatto in JavaScript puro, direttamente nel browser.

---

# PNG IPTC Tagger (English)

Browser-based tool for writing IPTC (and XMP) metadata directly into PNG files, without converting them to another format. Built for cutout PNGs (with transparency) used in Panini's production materials.

**Zero installation.** Open the page, drag in your files, download the result. Everything runs in your browser: no file is uploaded to any external server.

🔗 **Open the tool:** _(link to the GitHub Pages page, e.g. `https://<your-username>.github.io/<repo-name>/`)_

---

## How to use it

1. **Upload your PNGs** — drag one or more files into the upload area, or click to pick them from your computer.
2. **Fill in the IPTC fields:**
   - **Title** — the image's title
   - **Description** — description/caption
   - **Description Writer** — who wrote or reviewed the caption
   - **Keywords** — comma-separated keywords
   - **Instructions** — internal usage instructions
3. **(Optional) Use placeholders** to auto-fill fields based on the file name, folder, or a running counter — same syntax as ACDSee's placeholders. Available placeholders:
   - `<File Properties:Filename>` — full file name
   - `<File Properties:Filename (w/o extension)>` — file name without extension
   - `<File Properties:Extension>` — extension
   - `<File Properties:Folder>` — source folder (when available)
   - `<Counter>`, `<Counter:2>`, `<Counter:3>` — running number within the batch (1, 01, 001…)
   - `<Content:Title>`, `<Content:Description>` — reuse the value already typed in another field
4. **Click "Write IPTC and download".** With a single file you get the tagged PNG directly; with multiple files you get a ZIP containing all the tagged files.

The original files are never modified: the tool always produces copies.

## Compatibility

Metadata is written in two formats in parallel, for maximum compatibility:

| Tool field | Legacy IPTC tag | XMP tag |
|---|---|---|
| Title | Object Name | `dc:title` |
| Description | Caption-Abstract | `dc:description` |
| Description Writer | Writer/Editor | `photoshop:CaptionWriter` |
| Keywords | Keywords | `dc:subject` |
| Instructions | Special Instructions | `photoshop:Instructions` |

The data can be read with ExifTool, Adobe Bridge, Photoshop, ACDSee, and most DAM systems. Re-tagging a file already processed by this tool replaces the previous metadata rather than duplicating it.

## Technical notes

PNG has no native chunk for classic IPTC-IIM. This tool works around that by following the same convention used by ExifTool and ImageMagick: IPTC data is wrapped in a Photoshop (8BIM) block inside a PNG `zTXt` chunk labeled `Raw profile type iptc`, while XMP is written into a standard `iTXt` chunk. No format conversion, no external dependency to install: all PNG chunk handling is done in plain JavaScript, entirely in the browser.
