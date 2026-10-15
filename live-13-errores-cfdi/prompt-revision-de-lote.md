# Lo timbrado contra lo registrado: el prompt de revisión de lote

Jueves de ContadorIA · 15 de octubre de 2026 · Serie "Cuando el algoritmo ya te señaló"
Serie presentada por Certera.

Un prompt que se corre cada mes, dentro del proyecto de Claude del cliente (las
instrucciones del proyecto son las del [jueves 1 de octubre](../live-11-carta-invitacion/)).

Si lo vas a correr cada mes, conviene instalarlo como **skill**, como la del
jueves 8: las mismas reglas, en [`revision-de-lote/SKILL.md`](revision-de-lote/SKILL.md), y cómo
instalarla en el [README](README.md#la-skill).

---

## Qué subes

1. **CFDI emitidos** del mes (el Excel de la descarga masiva, con estatus).
2. **CFDI recibidos** del mes y de los primeros días del mes siguiente (ahí
   llegan las facturas de operaciones del mes que cierras).
3. **El registro contable**: las pólizas del mes exportadas de tu sistema, con
   el UUID de cada una.

## El prompt

```
Revisa el lote de [mes y año]: lo que el SAT tiene contra lo que mi sistema
registró.

Reglas del cruce:
- La llave es el UUID. Una póliza sin UUID es "registro sin CFDI".
- Ingreso del SAT: CFDI tipo I vigentes, subtotal menos descuento. Los tipo E
  emitidos restan.
- Un CFDI cancelado no cuenta, aunque se haya cancelado después de registrar.
- Si un CFDI tiene relación 04 (sustitución), el que sustituye reemplaza al
  cancelado: solo uno de los dos debe estar registrado.
- Una nota de crédito RECIBIDA (tipo E de un proveedor) reduce compras o gastos,
  nunca ventas.
- Para gastos, usa el periodo de la operación (concepto, periodo que ampara,
  fecha de entrega), no la fecha de emisión. Si no puedes saber el periodo de
  la operación, dilo.

Entrégame:
1. Totales del mes: ingresos según el SAT, ingresos según mi sistema y la
   diferencia. Lo mismo para gastos, por fecha de emisión y por fecha de
   operación.
2. Una fila por hallazgo: UUID o póliza, tercero, monto, qué tipo de error es
   (no registrado, sin CFDI, monto distinto, cancelado vivo, sustitución
   duplicada, nota de crédito mal aplicada, periodo equivocado) y la
   corrección que propones en el sistema.
3. La suma de los hallazgos tiene que explicar la diferencia completa. Si no
   la explica, dime cuánto queda sin explicar.
4. Las preguntas para el cliente, redactadas, para lo que no se resuelve con
   los archivos.

No corrijas nada por tu cuenta ni supongas montos. Esto es la revisión; las
pólizas las corrijo yo.
```

## Por qué funciona

El SAT no lee tu sistema contable: lee tus CFDI. Cada póliza que no cuadra con
un UUID es una diferencia que él ve y tú no. Este prompt hace el cruce por
UUID, que a mano nadie aguanta en el lote número cuarenta.

## Antes de usarlo con datos reales

Pruébalo con datos ficticios, dentro de la cuenta correcta. El tratamiento
fiscal de la fecha de operación de un gasto confírmalo con tu criterio y la
disposición aplicable: el prompt ordena, no decide.
