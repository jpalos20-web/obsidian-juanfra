---
title: "Reconciliación de gastos e ingresos en Notion"
uuid: 96882aec-134a-44e6-b338-4a63caa31b07
fecha: 2026-07-03
fuente: conversations.json
tags:
  - transcripcion
---

# Reconciliación de gastos e ingresos en Notion

*Conversación completa, 2026-07-03. Exportada de Claude.ai, sin resumir.*

---

### 🧑 Juanfra

necesito cruzar datos y asegurarme de que en mi notion están todos los movimientos de gastos e ingresos de mi cuenta de ing, tengo que cuadrar al centimo mi notion

---

### 🤖 Claude

I should examine the CSV file the user uploaded since it's likely the Notion export they mentioned.
```
This block is not supported on your current device yet.
```

I'm noticing the CSV only contains income entries from a Notion export with 64 data rows, while the PDF has hundreds of transactions spanning both income and expenses from December 2025 through July 2026. The user needs to verify that every single movement from their ING account—both inflows and outflows—is recorded in Notion to reconcile down to the exact cent, but the current data is incomplete since it's missing all the expense entries.

My approach is to extract all the PDF transactions I already have and systematically match them against the CSV by comparing dates, descriptions, and amounts to identify what's missing from Notion and create a detailed reconciliation report. First, I need to examine the full CSV to confirm it's truly income-only and see what date range it actually covers.
```
This block is not supported on your current device yet.
```

I'm looking at the user's Notion income database covering January through July 2026 with 64 entries, but they need to reconcile both income and expenses against their bank account to verify everything matches down to the cent—the expenses are in a separate database they haven't uploaded yet.

Since I only have the income CSV, I should extract all transactions from the PDF bank statement they provided and parse out the income entries to compare against Notion, then ask if they want to upload the expenses data too for a complete reconciliation.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

I'm noticing the table extraction is dropping some rows—there are only 254 rows per page including headers, but I'm seeing missing entries like the first "Pago en Revolut" transaction that should be there. I should switch to extracting raw text per page and parsing with regex instead, or clean up how headers repeat across pages and count the actual data rows more carefully.
```
This block is not supported on your current device yet.
```

The table extraction is only capturing 197 rows when there are actually over 230 transactions in the document, so I'm missing some entries like the Revolut payment and certain date rows. Since the text version is already complete and cleaner, I should parse it directly using regex to extract the transaction blocks marked by the "F. VALOR CATEGORÍA..." pattern instead of relying on the table extraction.
```
This block is not supported on your current device yet.
```

Good, plain text extraction is much cleaner. Now let me parse this into structured rows.
```
This block is not supported on your current device yet.
```

I'm noticing the PDF structure has both image-rendered tables and text versions below them, but the text versions don't include amounts—just categories and descriptions—so they wouldn't match the date regex pattern I'm using. Let me reconsider whether those duplicate entries are actually being counted in the 395 total.
```
This block is not supported on your current device yet.
```

I'm noticing a discrepancy—19 pages with 19 unique occurrences should give me around 197 entries, but I'm getting 395 instead. This suggests the extraction might be splitting entries incorrectly, possibly when descriptions span multiple lines or contain embedded amounts that match date patterns. Let me print out all the entries to spot what's causing the duplication and identify any anomalies, especially unusually short ones.
```
This block is not supported on your current device yet.
```

I'm realizing this is just a formatting issue with how multi-line descriptions wrapped—the actual transaction count of 395 seems inflated because my regex-based date splitting is incorrectly treating wrapped description lines as separate entries, so I need to check whether entries are actually missing date markers at the start or if the multi-line descriptions are just bleeding into the next transaction.

Let me directly scan through the full text more carefully and print out a sample of entries around the 190-220 range to verify the actual count against what I'd expect from the page count.
```
This block is not supported on your current device yet.
```

The count of 395 transactions checks out against the document structure—with roughly 19 page pairs and about 20-22 rows visible per page, that gives me the expected range of 380-420 entries, so my earlier estimate was off but the actual data aligns well.

Now I need to parse each entry cleanly by extracting the date, category, subcategory, description, amount, and balance. The tricky part is that descriptions sometimes wrap across lines and include AEAT information, but the amounts typically appear on the first line. I'll collapse newlines to spaces within each entry and use regex to capture the date, the middle section (which bundles category, subcategory, and description together), and the amount and balance at the end. Since my main goal is reconciling against the Notion CSV which only tracks income entries, I really just need to extract the positive transactions with their date, description, and amount—the full category breakdown isn't essential for matching purposes.
```
This block is not supported on your current device yet.
```

I see the issue now—when I'm concatenating lines within each entry, descriptions from one entry are bleeding into the next because the PDF's multi-column layout puts amounts and balances on the right side while the next row's text starts fresh, but my regex expects a clean sequence of description, amount, and balance at the end, which breaks when that order gets scrambled by the line joining.

Rather than wrestling with text extraction and regex patterns, I should switch to using extract_words with x,y coordinates to reconstruct rows by grouping words that share similar vertical positions, then sort them left-to-right. This respects the actual column layout regardless of how the PDF's text wrapping jumbles the extraction order.
```
This block is not supported on your current device yet.
```

Now I'll group words by row (top coordinate) and reconstruct each row properly using x-position column boundaries.
```
This block is not supported on your current device yet.
```

I've confirmed 395 transaction rows and now I'm working through the column boundaries to parse each row—mapping out where VALOR, CATEGORIA, SUBCATEGORIA, DESCRIPCION, COMENTARIO, IMPORTE, and SALDO fall based on their x-position ranges, then assigning words to the correct columns using x0 thresholds and midpoints between boundaries.
```
This block is not supported on your current device yet.
```

All 395 rows parsed cleanly. Now let's convert to numeric and save.
```
This block is not supported on your current device yet.
```

I need to verify the chain consistency by checking whether each balance minus its corresponding transaction amount equals the next balance, since the rows are ordered from newest to oldest.
```
This block is not supported on your current device yet.
```

Extracción perfecta: los 395 movimientos casan exactamente saldo a saldo, sin errores. Ahora comparo contra tu Notion.
```
This block is not supported on your current device yet.
```

I'm noticing the CSV file only contains income entries—65 rows total—but the user asked me to reconcile both expenses and income. Since I don't have their gastos export from Notion, I can only fully reconcile the income side; I'll need them to provide the expenses file to complete the full reconciliation. Let me start by matching the income entries from the PDF against what's in this CSV.

I'm comparing the PDF's 76 income entries (totaling 28,018.46) against the Notion CSV's 65 rows (totaling 24,881.70), with a difference of about 3,136.76. Some Notion entries combine multiple sub-items that appear separately in the PDF, so I'll need to account for that when matching. I'll write a matching algorithm that pairs PDF entries with Notion entries by date and amount, allowing for minor date offsets since Notion might record dates differently than the PDF source.

Writing matching script...
```
This block is not supported on your current device yet.
```

Looking at the reconciliation, I'm noticing that what appeared to be missing entries are actually combined in Notion—like the two Helena Pont de Roda payments (460 + 500) merged into a single 960 entry, and the AEAT devolución amounts (100 + 100) consolidated into one 200 row. So the data does match up, just organized differently between the two systems.

However, there's a genuine gap: the December 2025 entries (two 100 AEAT devoluciones on 23/12/2025) don't appear in Notion at all because the CSV only starts from January 7, 2026—so those are truly missing from the Notion records, not just combined.

For the 16/05/2026 Wallapop entry, it looks like there's only one 5€ transaction in the PDF (a Bizum from Federico with "flash" in the description), but Notion has split this into two separate entries—one as the Bizum and another as "Venta Flash Wallapop"—creating a duplicate that doesn't actually exist in the source data. I need to dig into the raw PDF rows for those problematic entries to see how the multi-line descriptions are actually being parsed, since text wrapping across columns is causing the descripcion field to get misaligned—especially when entries like "Transferencia recibida de..." wrap to new lines but fall under different column positions than expected.
```
This block is not supported on your current device yet.
```

I'm confirming these are legitimate ING transactions where the AEAT tax refund pairs (100+100 entries combined as 200 in Notion) match up for January 22nd, March 24th, and February 26th. The December 23rd, 2025 pair doesn't have a corresponding Notion entry because the CSV data only goes back to January 7th, 2026, so that's a real gap in the records.

The Amazon refund on March 18th for 1,679.99 is a significant missing entry—a large refund that should have been tracked but isn't in Notion. The Apple refund on February 19th for 2.99 is minor and probably not worth worrying about. More concerning are the two insurance refunds from FIATC SEGUROS on March 23rd and 27th, each for 604.39—both appearing in ING but neither in Notion's income list, which means over 1,200 in refunds are unaccounted for. I'm also checking a Bizum transfer from Federico on May 16th for 5.00 that appears to have some formatting inconsistency between the raw data and Notion. I'm realizing this is a case where Notion has recorded the same transaction twice—both "Bizum recibido de FEDERICO NICOLAS SCHECHTEL TRAVERSO" and "Venta Flash Wallapop" for 5€ on May 16th—but the PDF only shows one actual 5.00 income entry on that date. Since the PDF's balance chain is validated and complete, this means Notion is overstating income by 5€, likely due to a duplicate entry that should be flagged. Now I need to handle the combinable cases like Helena Pont and AEAT pairs with proper merging logic to avoid false positives, then generate the final gap report. I should also note that only the Ingresos file was provided for reconciliation, and I'll need to ask about the Gastos data if they want expenses reconciled too. Let me verify the ending balance checks as well to ensure everything ties out correctly. Continuing through the remaining unmatched entries: the Amazon refund on 18/03 and FIATC insurance refunds are genuine missing income items, along with the small Apple refund on 19/02. The 23/12/2025 AEAT pair likely falls outside the export range rather than being a true gap. I'm also noting a probable duplicate where the 16/05 Wallapop entry appears twice, and flagging that the 12/04 Bizum from Alba is actually a personal transfer between accounts (expense paired with income on the same day), so it makes sense it's not tracked as income. Still working through the remaining Bizum entries to verify which ones genuinely lack Notion matches. Computing the totals programmatically...
```
This block is not supported on your current device yet.
```

I'm noticing a discrepancy in my calculations—the remaining PDF gap of 2896.76 doesn't match my manual arithmetic, so I should verify this with code to avoid the errors I've been making with hand calculations.
```
This block is not supported on your current device yet.
```

Got a clean reconciliation now—about 3,141.76 in unmatched PDF income and one duplicate 5€ entry in Notion. For the report, I need to explain that the CSV only contains income data with no expenses, so I can only validate the ingresos side and will need the gastos export to complete the picture. I'll present the findings directly in Spanish, listing out the genuinely missing income entries with their dates and amounts.

I should flag that 5€ Wallapop entry as a likely duplicate, and note the 12/04 and 22/02 Bizums (5€ and 45€) that have matching outgoing transfers the same day—those are mutual reimbursements, not real income. Then I'll ask for the Gastos CSV to finish the reconciliation. Given the preference for directness, I'll keep it concise with a compact table summary rather than lengthy explanation.He cruzado los 395 movimientos del PDF de ING (validé la cadena de saldos, encaja al céntimo) contra tu CSV de Notion. Aviso importante primero:

**El CSV que subiste solo contiene Ingresos** (65 filas, del 07/01/2026 al 02/07/2026). No hay export de Gastos, así que de momento solo puedo cuadrar la parte de ingresos. Si me pasas el export de tu tabla de Gastos, cuadro también esa parte.

**Resultado ingresos:**
- ING (positivos): 76 movimientos, 28.018,46 €
- Notion: 65 filas, 24.881,70 €

Después de emparejar por fecha+importe (y agrupando los casos que Notion registra en una sola fila, como el pago de boda Helena/Enrique o las devoluciones AEAT de 100+100€), esto es lo que falta de verdad en Notion:

| Fecha | Importe | Concepto (ING) |
|---|---|---|
| 18/03/2026 | 1.679,99 € | Devolución tarjeta WWW.AMAZON.* R95A986R5 |
| 23/03/2026 | 604,39 € | Devolución recibo FIATC SEGUROS |
| 27/03/2026 | 604,39 € | Devolución recibo FIATC SEGUROS (segunda) |
| 19/02/2026 | 2,99 € | Devolución tarjeta APPLE.COMBILL |
| 23/12/2025 | 100,00 € | Devolución AEAT (DES) |
| 23/12/2025 | 100,00 € | Devolución AEAT (FNG, familia numerosa) |

**Total que falta: 3.141,76 €** (los dos últimos de dic-2025 pueden ser simplemente porque tu export de Notion no llega hasta esa fecha, no necesariamente un error real).

Dos más para revisar, no metidos en la tabla porque son casos límite:
- **22/02/2026, 5€** Bizum de Antonio Landeira — ese mismo día le mandaste otros 5€. Reembolso mutuo, probablemente correcto que no esté como ingreso.
- **12/04/2026, 45€** Bizum de Alba Escalante — mismo día le mandaste 45€ también. Mismo caso, transferencia interna, no ingreso real.

**Posible duplicado en Notion:** tienes "Venta Flash Wallapop, 5,00€, 16/05/2026" pero en ING ese día solo hay un ingreso de 5€ (el Bizum de Federico Schechtel). Parece que Notion cuenta dos veces esos 5€ cuando en el banco solo entró una vez.

¿Quieres que te pase esto en una tabla/archivo descargable, o prefieres que primero me pases el export de Gastos para hacer el cuadre completo?

---
