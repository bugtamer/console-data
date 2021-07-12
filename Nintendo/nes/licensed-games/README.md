# NES Licensed Games

| File                                                       | Purpose                                                |
| ---------------------------------------------------------- | ------------------------------------------------------ |
| [nes_games.pdf](./nes_games.pdf)                           | Original file from data source                         |
| [nes_games.adobe-reader.txt](./nes_games.adobe-reader.txt) | Intermediate raw text file                             |
| [nes_games.brandfolder.txt](./nes_games.brandfolder.txt)   | Intermediate raw text file                             |
| [licensed-games.csv](./licensed-games.csv)                 | Strutured final file (from nes_games.adobe-reader.txt) |


## Table Of Content

- [Data Source](#data-source)
- [Process Data Source](#process-data-source)
  - [Extract text from data source](#extract-text-from-data-source)
  - [Convert text to csv](#convert-text-to-csv)
  - [Change release date format](#change-release-date-format)
    - [Regex strategy](#regex-strategy)
    - [Spreadsheet strategy](#spreadsheet-strategy)

## Data Source

- [http://www.nintendo.com/doc/nes_games.pdf (2007-01-21) at Internet Archive](https://web.archive.org/web/20070121012513/http://www.nintendo.com:80/doc/nes_games.pdf) 2021-07-12

## Process Data Source

### Extract text from data source

- Adobe Reader `Save as Text...`
- [Brandfolder Text Extractor Tool](https://brandfolder.com/workbench/extract-text-from-image) 2021-07-11
- Save result as: [nes_games.txt](./nes_games.txt)
  - Encoding: UTF-8
  - EOL: `\n`

### Convert text to csv

- Open [Visual Studio Code](https://code.visualstudio.com/)
- Replace with Regular Expressions activated:
  | Regex to find                           | Replace by                | Explanation                                                       |
  | --------------------------------------- | ------------------------- | ----------------------------------------------------------------- |
  | `\u000C`                                |                           | (2) Remove `U+000C` Form Feed. (3)                                |
  | `^(.+)\s$`                              | `$1`                      | (2) Remove trailing spaces                                        |
  | `(Title:)\n(Licensee)\n(Released\n)`    | `$1 $2 $3`                | (2) Left `Title`, `Licensee` & `Released` in a single line        |
  | `completeoldgameslist.xls\n`            |                           | (1) Remove line `completeoldgameslist.xls`.                       |
  | `^\n`                                   |                           | Remove blank lines but last                                       |
  | `NES Games\n`                           |                           | Remove all lines of `NES Games`                                   |
  | `\s,`                                   | `,`                       | Remove extra space before comas                                   |
  | `Title: Licensee Released\n`            |                           | Remove all lines (keep the first one): `Title: Licensee Released` |
  | `Title: Licensee Released`              | `Title;Licensee;Released` | CSV header is already set                                         |
  | `\s(\w+\s\d{4}$)`                       | `;$1`                     | Replace the space before the `Release` date with a semicolon (;)  |
  | `\s(Absolute)`                          | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Acclaim)`                           | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Activision)`                        | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(American Sammy)`                    | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(American Softworks)`                | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(American Technos)`                  | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Ascii)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Asmik)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Atlus Software)`                    | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Bandai)`                            | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Broderbund)`                        | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Bullet Proof Software)`             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Capcom)`                            | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Culture Brain)`                     | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Data East)`                         | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(EA Sports)`                         | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Electro Brain)`                     | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Electronic Arts)`                   | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Enix)`                              | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(FCI)`                               | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Gametek)`                           | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Hal America)`                       | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Hi-Tech)`                           | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Hot-B)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Hudson Soft)`                       | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(INTV)`                              | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Irem)`                              | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(JVC)`                               | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Jaleco)`                            | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Kemco)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Koei)`                              | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Konami)`                            | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(LJN)`                               | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Matchbox Toys)`                     | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Mattel Inc.)`                       | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Meldac)`                            | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Microprose)`                        | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Milton Bradley)`                    | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Mindscape)`                         | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(NTVIC)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Namco)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Natsume)`                           | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Nintendo)`                          | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Ocean)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Parker Brothers)`                   | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Romstar)`                           | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(SNK)`                               | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Seika)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Seta)`                              | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Sofel)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Sony Imagesoft)`                    | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Square Soft)`                       | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Sunsoft)`                           | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(THQ)`                               | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Taito Software)`                    | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Taxan)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Tecmo)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Titus)`                             | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Toho)`                              | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Tradewest)`                         | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Triffix)`                           | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(UBI Soft)`                          | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Ultra Soft)`                        | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Vic Tokai)`                         | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  | `\s(Virgin Interactive)`                | `;$1`                     | Replace the space before the `Licensee` with a semicolon (;)      |
  - (1) Required only when the `nes_games.txt` comes from `Brandfolder Text Extractor Tool`.
  - (2) Required only when the `nes_games.txt` comes from an `Adobe Reader` extraction.
  - (3) [What Unicode character is this?](https://babelstone.co.uk/Unicode/whatisit.html)
 - Save it as `nes_games.csv`

### Change release date format

- Choose one strategy: Replace with regex or Spreadsheet

#### Regex strategy

| Regex to find                  | Replace by                                           | Notes                         |
| ------------------------------ | ---------------------------------------------------- | ----------------------------- |
| `Title;Licensee;Released`      | `Title;Licensee;Released;Release Year;Release Month` | Add Release Year and Month    |
| `(.+;.+;)(January)\s(\d{4})`   | `$1$2 $3;$3;01`                                      | Replace `January` with `01`   |
| `(.+;.+;)(February)\s(\d{4})`  | `$1$2 $3;$3;02`                                      | Replace `February` with `02`  |
| `(.+;.+;)(March)\s(\d{4})`     | `$1$2 $3;$3;03`                                      | Replace `March` with `03`     |
| `(.+;.+;)(April)\s(\d{4})`     | `$1$2 $3;$3;04`                                      | Replace `April` with `04`     |
| `(.+;.+;)(May)\s(\d{4})`       | `$1$2 $3;$3;05`                                      | Replace `May` with `05`       |
| `(.+;.+;)(June)\s(\d{4})`      | `$1$2 $3;$3;06`                                      | Replace `June` with `06`      |
| `(.+;.+;)(July)\s(\d{4})`      | `$1$2 $3;$3;07`                                      | Replace `July` with `07`      |
| `(.+;.+;)(August)\s(\d{4})`    | `$1$2 $3;$3;08`                                      | Replace `August` with `08`    |
| `(.+;.+;)(September)\s(\d{4})` | `$1$2 $3;$3;09`                                      | Replace `September` with `09` |
| `(.+;.+;)(October)\s(\d{4})`   | `$1$2 $3;$3;10`                                      | Replace `October` with `10`   |
| `(.+;.+;)(November)\s(\d{4})`  | `$1$2 $3;$3;11`                                      | Replace `November` with `11`  |
| `(.+;.+;)(December)\s(\d{4})`  | `$1$2 $3;$3;12`                                      | Replace `December` with `12`  |
| `^(.+;.+;)(\d{2})\s(\d{4})$`   | `$1$3-$2`                                            | Change Release Date order     |
- Save it as `nes_games.csv`

#### Spreadsheet strategy

- Open [`LibreOffice Calc`](https://www.libreoffice.org/download/download/)
- Menu `Open...`
  - Select `nes_games.csv` file.
  - It will appear the `Text Import - [nes_games.csv]` modal.
  - In the section `Separator Options`, choose `Separated by` and check only `Semicolon`. Finally, click on `Ok`.
- `nes_games.csv` file is now ready with this info:
  - The column `A` has the game Titles.
  - The column `B` has the licensees.
  - The column `C` holds the released dates.
- Add new headers
  - Add `Year` to `D1` cell.
  - Add `Month number` to `E1` cell.
  - Add `Month name` to `F1` cell.
- Add new `Formula`
  - Add `= RIGHT(C2; 4)` to `D2` cell.
  - Add `= LEFT(C2; LEN(C2) - 5)` to `F2` cell.
  - Add `= SWITCH(F2; "January"; "01"; "February"; "02"; "March"; "03"; "April"; "04"; "May"; "05"; "June"; "06"; "July"; "07"; "August"; "08"; "September"; ; "October"; "10"; "November"; "11"; "December"; "12")` to `E2` cell.
- Select from `D2` to `F2` and apply these formulas to entire columns.
- Hide Column `C`
- Menu `File`, click on `Save as...`and
  - Save it as `nes_games.ods`.
  - Save it as `nes_games.csv`. `TextCSV (.csv)`
    - Character set: `Unicode (UTF-8)`
    - Field delimiter: `;`
    - Stringdelimiter: Empty
    - [X] Save cell content as shown
    - [ ] Save cell formulas instead of calculated values
    - [ ] Quote all text cells
    - [ ] Fixed column width
    - Click on `OK`