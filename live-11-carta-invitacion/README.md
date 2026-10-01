# Episodio 11 · Carta invitación: encuéntrala tú primero

Primer episodio de la serie **«Cuando el algoritmo ya te señaló»**. Serie
presentada por Certera.

La carta invitación llega cuando el SAT cruzó tres números que ya tiene y no
le cuadraron: lo que facturaste, lo que declaraste y lo que te depositaron.
La idea del episodio en una línea: **esa conciliación la puedes hacer tú
primero, cada mes, en diez minutos por cliente.**

## Qué hay aquí

| Archivo | Qué es |
|---|---|
| [`prompt-conciliacion-tres-vias.md`](prompt-conciliacion-tres-vias.md) | Las instrucciones del proyecto de Claude y el prompt de cada mes, listos para copiar. |
| [`datos/cfdi-emitidos-ficticio.csv`](datos/cfdi-emitidos-ficticio.csv) | Los CFDI emitidos de julio a septiembre de 2026: 9 de ingreso y 1 complemento de pago. Uno está cancelado. |
| [`datos/complementos-de-pago-ficticio.csv`](datos/complementos-de-pago-ficticio.csv) | El complemento de pago de la factura PPD. |
| [`datos/estado-de-cuenta-ficticio.csv`](datos/estado-de-cuenta-ficticio.csv) | Los depósitos del banco en esos tres meses. |
| [`datos/declaraciones-ficticio.csv`](datos/declaraciones-ficticio.csv) | Los ingresos declarados para ISR, mes por mes. |

**Todo es inventado.** El contribuyente es una persona física con actividad
empresarial que no existe, y los clientes se llaman Alfa, Beta, Gamma, Delta
y Epsilon a propósito.

## Cómo repetir el ejercicio

1. Crea un proyecto en Claude y pega las **instrucciones del proyecto** del
   archivo del prompt.
2. Sube los cuatro CSV de `datos/` al chat del proyecto.
3. Pega el **prompt de cada mes** y compara lo que te devuelve contra la
   lista de abajo.

Con tus datos reales, primero decide con qué cuenta van (el episodio del 24
de septiembre, «¿Qué hace la IA con tus datos?», es justo eso), y prueba el
prompt con estos datos antes de usar los de un cliente.

## Qué tiene que salir

Si el resultado no trae esto, el problema fue el prompt, no la base. Vuelve a
pedirlo.

| Mes | Facturado vigente | Cobrado | Declarado | Depósitos |
|---|---|---|---|---|
| Julio | 65,000 | 35,000 | 35,000 | 65,600 |
| Agosto | 32,000 | 62,000 | 32,000 | 151,920 |
| Septiembre | 53,000 | 53,000 | 35,000 | 61,480 |

Montos de ingreso sin IVA; los depósitos traen IVA.

Y las diferencias, cada una en su grupo:

1. **Julio, traspaso de 25,000** de una cuenta propia. Se deposita pero no es
   ingreso: **se documenta** con el estado de cuenta de origen.
2. **Julio, la factura PPD de Gamma (30,000)** no cuenta en julio: se cobró en
   agosto. **Se explica sola.**
3. **Agosto, ese mismo cobro de Gamma no se declaró.** El complemento es del
   20 de agosto, así que es ingreso de agosto. **Se corrige** con
   complementaria. Es el que no ves si comparas facturado contra declarado:
   agosto «cuadra» y no está bien.
4. **Agosto, depósito en efectivo de 80,000.** Un préstamo, según el cliente.
   No es ingreso, pero el banco lo reporta: **se documenta** con el contrato.
5. **Septiembre, la factura de Epsilon (18,000) no se declaró.** **Se
   corrige.**
6. **Septiembre, la factura de Beta del 22 está cancelada** y se volvió a
   emitir el 25. La cancelada no cuenta, y el prompt te dice cuál fue.

## Lo que este prompt sí hace y lo que no

Arma la tabla, explica cada diferencia y te dice qué le preguntarías al
cliente. **No calcula impuesto a cargo** y no decide por ti qué se corrige:
eso, y la firma, siguen siendo tuyos.
