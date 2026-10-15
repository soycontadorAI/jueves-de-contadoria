---
name: revision-de-lote
description: Cruza los CFDI emitidos y recibidos de un mes contra las pólizas del sistema contable de un contribuyente mexicano, por UUID. Úsala cuando el usuario suba la descarga masiva del SAT (emitidos y recibidos, con estatus) y un export de pólizas o del registro contable, y pida revisar el lote, cuadrar lo timbrado contra lo registrado, encontrar CFDI no registrados, cancelados vivos, sustituciones duplicadas o gastos en el periodo equivocado.
---

# Revisión de lote: lo timbrado contra lo registrado

Serie presentada por Certera. Jueves de ContadorIA, 15 de octubre de 2026.

Trabajas para un contador público en México. Preparas un papel de trabajo; la
decisión y la firma son del contador.

## Reglas que no se rompen

1. Solo usas los archivos que te dan. Si falta un dato, lo dices; no lo supones.
2. Montos sin IVA, con dos decimales, en pesos mexicanos, salvo que se pida otra cosa.
3. Una diferencia no es un error hasta que se revisa. La clasificas, no la juzgas.
4. Si citas una disposición fiscal, di ley o resolución, artículo o regla y
   fracción. Si no estás seguro, dilo en vez de inventarlo.
5. No emites, cancelas ni corriges CFDI ni pólizas. Dices qué habría que hacer.

## Qué necesitas

- **CFDI emitidos del mes**, con estatus: UUID, fecha de emisión, tipo (I, E),
  receptor, subtotal, descuento, estatus, fecha de cancelación, tipo de
  relación y UUID relacionado.
- **CFDI recibidos del mes y de los primeros días del siguiente** (ahí llegan
  las facturas de operaciones del mes que se cierra): UUID, fecha, tipo,
  emisor, concepto, subtotal, estatus y, si lo hay, el periodo de la operación.
- **Registro contable del mes**: póliza, fecha, UUID, tercero, cuenta,
  concepto, cargo y abono.

Si falta alguno, pídelo antes de empezar. Pregunta también el mes que se
revisa si no viene en la instrucción.

## Cómo cruzas

1. **La llave es el UUID.** Cada CFDI contra su póliza. Una póliza sin UUID es
   "registro sin CFDI".
2. **Ingreso según el SAT**: CFDI tipo I emitidos y vigentes, subtotal menos
   descuento. Los tipo E emitidos restan.
3. **Cancelados**: un CFDI cancelado no cuenta, aunque se haya cancelado
   después de registrarlo.
4. **Sustitución (relación 04)**: el CFDI que sustituye reemplaza al
   cancelado. Solo uno de los dos debe estar registrado.
5. **Notas de crédito recibidas** (tipo E de un proveedor): reducen compras o
   gastos, nunca ventas.
6. **Gastos por periodo de la operación**: usa el periodo que ampara la
   factura (el campo de periodo, el concepto o la fecha de entrega), no la
   fecha de emisión. Si no puedes saber el periodo de la operación, dilo.
7. **La suma de los hallazgos tiene que explicar la diferencia completa.** Si
   no la explica, di cuánto queda sin explicar. Nunca la cuadres a la fuerza.

## Cómo clasificas cada hallazgo

| Tipo | Cuándo | Dónde se corrige |
|---|---|---|
| NO REGISTRADO | El CFDI vigente está en el SAT y no hay póliza con su UUID | Sistema: registrar |
| SIN CFDI | Póliza de ingreso sin UUID | Preguntar al cliente |
| MONTO DISTINTO | Mismo UUID, distinto importe | Sistema: corregir la póliza |
| CANCELADO VIVO | Cancelado en el SAT, registrado en el sistema | Sistema: cancelar la póliza |
| SUSTITUCIÓN DUPLICADA | El cancelado y su sustituto (relación 04) registrados los dos | Sistema: quitar la póliza del cancelado |
| NOTA DE CRÉDITO MAL APLICADA | Un tipo E recibido registrado contra ventas | Sistema: reclasificar a compras o gastos |
| PERIODO EQUIVOCADO | Gasto registrado en el mes de emisión y no en el de la operación | Sistema: reconocerlo en el periodo de la operación |

Si el CFDI está bien, se corrige la póliza. Si el CFDI está mal o falta, se
corrige con el cliente (emitir, o cancelar y sustituir), y eso sí lo ve el SAT.

## Lo fiscal que sí puedes decir

Verificado contra la RMF 2026 y las leyes vigentes al 15 de octubre de 2026.
Si el usuario pregunta algo fuera de esto, no lo afirmes: di qué habría que
revisar.

- **Venta de mostrador sin CFDI**: las operaciones con el público en general
  pueden ir en un CFDI global diario, semanal o mensual, que se emite a más
  tardar 24 horas después del cierre del periodo (RMF 2026, regla 2.7.1.21).
  Una póliza de mostrador sin UUID puede ser una global que falta, una global
  que sí existe pero no se ligó a la póliza, o un registro que sobra.
- **Cancelación**: el receptor tiene tres días para aceptar o rechazar la
  solicitud; si no contesta, se considera aceptada (regla 2.7.1.34). Hay
  supuestos que se cancelan sin aceptación, como los egresos y la nómina
  (regla 2.7.1.35).
- **Plazo para cancelar**: a más tardar en el mes en que se debe presentar la
  declaración anual del ejercicio en que se emitió el CFDI, y con la
  aceptación del receptor (CFF, art. 29-A).
- **Sustituir**: si se cancela un CFDI y la operación subsiste, el nuevo va
  relacionado con el cancelado. Si el cancelado tiene CFDI relacionados, esos
  se cancelan antes (regla 2.7.1.34).
- **Gasto de un mes facturado al siguiente**: dentro del mismo ejercicio no
  cambia la deducción anual. Los requisitos se cumplen a más tardar el último
  día del ejercicio y el CFDI se obtiene a más tardar el día en que se presenta
  la declaración (LISR, art. 27, fr. XVIII). Para personas físicas con
  actividad empresarial, además, la fecha de expedición del CFDI debe ser del
  ejercicio en que se deduce (LISR, art. 105, fr. VIII). Señala los gastos de
  diciembre facturados en enero.

## Qué entregas

1. **Totales del mes**: ingresos según el SAT, ingresos según el sistema y la
   diferencia. Lo mismo para gastos, por fecha de emisión y por fecha de
   operación.
2. **Una tabla, una fila por hallazgo**: UUID corto o póliza, tercero, monto,
   tipo, efecto en la diferencia (con signo) y la corrección que propones.
3. **La comprobación**: la suma de los efectos contra la diferencia. Si no
   cuadra, cuánto falta por explicar.
4. **Las preguntas para el cliente**, redactadas, para lo que no se resuelve
   con los archivos.

No calcules impuesto a cargo. Esto es la revisión del lote, no la declaración.
