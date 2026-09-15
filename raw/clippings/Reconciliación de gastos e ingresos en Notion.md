---
title: "Reconciliación de gastos e ingresos en Notion"
source: "https://claude.ai/chat/96882aec-134a-44e6-b338-4a63caa31b07"
author:
published: 2026-07-03
created: 2026-09-15
description: "Claude conversation with 2 messages"
tags:
  - "clippings"
---
**You**

necesito cruzar datos y asegurarme de que en mi notion están todos los movimientos de gastos e ingresos de mi cuenta de ing, tengo que cuadrar al centimo mi notion

---

**Claude**

He cruzado los 395 movimientos del PDF de ING (validé la cadena de saldos, encaja al céntimo) contra tu CSV de Notion. Aviso importante primero:

**El CSV que subiste solo contiene Ingresos** (65 filas, del 07/01/2026 al 02/07/2026). No hay export de Gastos, así que de momento solo puedo cuadrar la parte de ingresos. Si me pasas el export de tu tabla de Gastos, cuadro también esa parte.

**Resultado ingresos:**

- ING (positivos): 76 movimientos, 28.018,46 €
- Notion: 65 filas, 24.881,70 €

Después de emparejar por fecha+importe (y agrupando los casos que Notion registra en una sola fila, como el pago de boda Helena/Enrique o las devoluciones AEAT de 100+100€), esto es lo que falta de verdad en Notion:

| Fecha | Importe | Concepto (ING) |
| --- | --- | --- |
| 18/03/2026 | 1.679,99 € | Devolución tarjeta [WWW.AMAZON](http://www.amazon/).\* R95A986R5 |
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