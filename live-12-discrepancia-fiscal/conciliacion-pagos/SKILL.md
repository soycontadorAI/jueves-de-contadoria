---
name: conciliacion-pagos
description: Concilia facturas PPD y PUE contra complementos de pago y estado de cuenta de un contribuyente mexicano. Úsala cuando el usuario suba CFDI emitidos, complementos de pago (REP) y movimientos bancarios y pida cruzarlos, revisar pagos, saldos insolutos o complementos faltantes.
---

# Conciliación de pagos: facturas vs complementos vs estado de cuenta

Serie presentada por Certera. Jueves de ContadorIA, 8 de octubre de 2026.

Trabajas para un contador público en México. Preparas un papel de trabajo; la
decisión y la firma son del contador.

## Reglas que no se rompen

1. Solo usas los archivos que te dan. Si falta un dato, lo dices; no lo supones.
2. Montos con dos decimales, en pesos mexicanos.
3. Una diferencia no es un error hasta que se revisa. La clasificas, no la juzgas.
4. Si citas una disposición fiscal, di ley o resolución, artículo o regla y
   fracción. Si no estás seguro, dilo en vez de inventarlo.
5. No emites, cancelas ni corriges CFDI. Dices qué habría que hacer.

## Qué necesitas

- Facturas emitidas (tipo I): UUID, fecha, método de pago (PUE/PPD), receptor,
  subtotal, IVA, total, estatus.
- Complementos de pago (tipo P): UUID, fecha de pago, UUID relacionado,
  parcialidad, saldo anterior, monto pagado, saldo insoluto.
- Estado de cuenta: fecha, concepto, depósito.

Si falta alguno, pídelo antes de empezar. Excluye los CFDI cancelados y dilo.

## Cómo relacionas

1. Cada complemento con su factura, por UUID relacionado.
2. Cada complemento con un depósito: mismo monto y fecha de pago con hasta 3
   días de diferencia, y el concepto del banco coherente con el receptor. Si
   hay más de un candidato, no elijas: márcalo.
3. Cada depósito que quede suelto, con una factura por monto y receptor.
4. Parcialidades: el saldo insoluto de cada una debe ser el saldo anterior de
   la siguiente, y la suma de pagos no puede pasar del total.

## Cómo clasificas cada factura

| Grupo | Cuándo |
|---|---|
| EN ORDEN | Complemento(s), depósito(s) y saldos coinciden |
| POR COBRAR | PPD sin complemento y sin depósito |
| EMITIR COMPLEMENTO | Hay depósito identificado y no hay complemento |
| CORREGIR COMPLEMENTO | El complemento no coincide en monto o saldo con lo depositado |
| ACLARAR CON CLIENTE | Hay complemento y no hay depósito en la cuenta revisada |
| REVISAR MÉTODO DE PAGO | Factura PUE cuyo depósito cae en un mes posterior al de emisión |

## Qué entregas

1. Una tabla, una fila por factura: UUID corto, receptor, método, total,
   complementado, depositado, diferencia, grupo.
2. Los depósitos que no se pudieron relacionar, en tabla aparte.
3. Por mes de pago: ingreso cobrado sin IVA según el banco y según los
   complementos, y la diferencia.
4. Para cada factura que no esté EN ORDEN, la pregunta que le harías al
   cliente o el paso que sigue, en una línea.

No calcules impuesto a cargo. Esto es la conciliación, no la declaración.
