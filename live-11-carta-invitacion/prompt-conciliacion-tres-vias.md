# La conciliación que dispara la carta invitación, hecha por ti primero

Jueves de ContadorIA · 1 de octubre de 2026 · Serie «Cuando el algoritmo ya te señaló»
Serie presentada por Certera.

Dos piezas: las **instrucciones del proyecto** (se configuran una vez por
cliente) y el **prompt** (se corre cada mes).

---

## 1. Instrucciones del proyecto

Crea un proyecto en Claude por cliente, nunca revuelto. En «Instrucciones del
proyecto» pega esto y cambia lo que va entre corchetes:

```
Eres mi auxiliar de revisión fiscal. Trabajas para un contador público en
México. El contribuyente de este proyecto es [persona física con actividad
empresarial / persona moral / RESICO], RFC [RFC].

Reglas que no se rompen:
1. Solo usas los archivos que te doy. Si falta un dato, lo dices; no lo supones.
2. Los montos se escriben con dos decimales y se suman en pesos mexicanos.
3. Una diferencia no es un error hasta que se revisa. La clasificas, no la juzgas.
4. Cuando cites una disposición fiscal, di ley, artículo y fracción. Si no
   estás seguro del artículo, dilo en vez de inventarlo.
5. La decisión y la firma son del contador. Tú preparas el papel de trabajo.
```

## 2. El prompt de cada mes

Sube cuatro archivos al chat del proyecto: CFDI emitidos (el Excel de la
descarga masiva), complementos de pago, estado de cuenta y el resumen de
declaraciones. Después:

```
Haz la conciliación de tres vías de [periodo]: lo facturado, lo declarado y
lo depositado.

Antes de comparar, normaliza:
- CFDI: solo tipo I vigentes. Excluye los cancelados aunque se hayan cancelado
  después de declarar, y dime cuáles fueron.
- Cobrado: los PUE cuentan en el mes de emisión; los PPD, en el mes de su
  complemento de pago.
- Depósitos: traen IVA. Compáralos contra el TOTAL cobrado, no contra el
  subtotal.
- Declarado: es sin IVA. Compáralo contra el SUBTOTAL cobrado.

Entrégame:
1. Una tabla por mes: facturado vigente, cobrado (subtotal y total),
   declarado, depósitos, y las dos diferencias (cobrado vs declarado,
   depósitos vs cobrado con IVA).
2. Por cada diferencia, una fila: monto, de dónde sale (UUID o movimiento
   del banco) y en qué grupo cae:
   - EXPLICADA: se aclara sola (timing de PPD, cancelación).
   - DOCUMENTAR: no es ingreso, pero hay que tener el soporte (traspaso,
     préstamo, reembolso).
   - CORREGIR: es ingreso y no se declaró.
3. Lo que no puedas explicar con los archivos, en una lista aparte, con la
   pregunta que le harías al cliente.

No calcules impuesto a cargo. Esto es la conciliación, no la declaración.
```

## Por qué funciona

El SAT ya tiene los tres números: tus CFDI, tus declaraciones y lo que el
banco informa. La carta invitación llega cuando **él** hizo este cruce y no
cuadró. Este prompt te deja hacerlo antes, cada mes, y llegar con la
diferencia explicada o corregida.

## Antes de usarlo con datos reales

Pruébalo primero con datos ficticios, dentro de la cuenta correcta. Revisa el
jueves del 24 de septiembre («¿Qué hace la IA con tus datos?») para decidir
con qué cuenta van los datos de tus clientes.
