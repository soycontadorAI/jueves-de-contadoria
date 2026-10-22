# Episodio 14 · IVA acreditable: revisar antes de que te revisen

Cuarto y último episodio de la serie **"Cuando el algoritmo ya te señaló"**.
Serie presentada por Certera. Invitado: **Miguel García**, contador y abogado
fiscalista ([MG Fiscal](https://mgfiscal.com.mx)).

Pedir una devolución de IVA es pedirle al SAT que revise. Él cruza tus CFDI,
su propio portal, lo que el banco le informa y su lista 69-B. La idea del
episodio en una línea: **haz ese cruce tú antes, y pide solo lo que resiste.**

## Qué hay aquí

| Archivo | Qué es |
|---|---|
| [`prompt-papel-de-trabajo-iva.md`](prompt-papel-de-trabajo-iva.md) | Las instrucciones del proyecto de Claude, el prompt del papel de trabajo y un ejemplo de lo que sale. |
| [`guia-documentacion-devoluciones-iva-mg-fiscal.pdf`](guia-documentacion-devoluciones-iva-mg-fiscal.pdf) | **La guía de Miguel:** cómo documentar una devolución de IVA. Lo que suelen requerir, la estructura de carpetas del expediente, los amarres antes de presentar, cómo atender un requerimiento y qué hacer si la niegan. |
| [`datos/cfdi-recibidos-ficticio.csv`](datos/cfdi-recibidos-ficticio.csv) | Los ocho CFDI recibidos en septiembre de 2026, como salen de la descarga. |
| [`datos/portal-sat-ficticio.csv`](datos/portal-sat-ficticio.csv) | Lo que muestra hoy el portal del SAT para esos mismos UUID. |
| [`datos/estado-de-cuenta-ficticio.csv`](datos/estado-de-cuenta-ficticio.csv) | Los movimientos del banco en septiembre. |
| [`datos/lista-69b-ficticio.csv`](datos/lista-69b-ficticio.csv) | La lista 69-B de la clase (un proveedor en definitivo). |
| [`datos/declaracion-septiembre-ficticio.csv`](datos/declaracion-septiembre-ficticio.csv) | Lo que se declaró en septiembre y la devolución que se pidió. |

**Los datos son inventados.** La comercializadora no existe, y los
proveedores se llaman Uno, Dos, Tres... a propósito. El 69-B también es de
mentira.

La guía es de Miguel y la comparte para este episodio. Es material de
carácter general: no sustituye el análisis de cada caso.

## Cómo repetir el ejercicio

1. Crea un proyecto en Claude y pega las **instrucciones del proyecto** del
   archivo del prompt. Si ya armaste el del
   [episodio 11](../live-11-carta-invitacion/), úsalo: las reglas son las
   mismas.
2. Sube los cinco CSV de `datos/` al chat del proyecto.
3. Pega el **prompt** y compara lo que te devuelve contra la tabla de abajo.

Con tus datos reales, primero decide con qué cuenta van (el episodio del 24
de septiembre, "¿Qué hace la IA con tus datos?", es justo eso), y prueba el
prompt con estos datos antes de usar los de un cliente.

## Qué tiene que salir

Si el resultado no trae esto, el problema fue el prompt, no la base. Vuelve a
pedirlo.

| | IVA |
|---|---|
| Lo que llegó (descarga) | 52,480.00 |
| Lo que muestra el portal hoy | 49,280.00 |
| Lo declarado | 46,080.00 |
| **Acreditable según la revisión** | **30,400.00** |
| IVA trasladado cobrado | 20,000.00 |
| Saldo a favor declarado (y pedido) | 26,080.00 |
| **Saldo a favor que resiste** | **10,400.00** |

La diferencia contra lo declarado, renglón por renglón:

1. **Proveedor Tres, 12,800.** PPD sin complemento y sin pago en el banco.
   No se acredita en septiembre: **se espera** al mes en que se pague.
2. **Proveedor Cuatro, 4,800.** Pagado, pero el proveedor está en el 69-B
   definitivo. **No se acredita** mientras no se acredite la materialidad.
3. **Proveedor Cinco, 3,200.** Vigente al descargar, cancelado hoy en el
   portal. **No se acredita.**
4. **Restaurante, 800.** El fin de semana del socio, con una tarjeta que no
   sale del banco de la empresa. **Se revisa** con el cliente: parece no
   deducible.
5. **Proveedor Siete, 480.** Pagado en efectivo, 3,480, arriba del tope.
   **No se acredita.**
6. **Proveedor Ocho, menos 6,400.** Pagado y vigente, pero **no se declaró**.
   Este suma a favor.

12,800 + 4,800 + 3,200 + 800 + 480 − 6,400 = **15,680.00**.

## Lo que este prompt sí hace y lo que no

Arma el papel de trabajo, clasifica cada CFDI y te dice qué le preguntarías
al cliente. **No decide** qué se acredita ni cuánto se pide: eso, y la firma,
siguen siendo tuyos.

Y si el requerimiento ya llegó, o la devolución se negó, el trabajo deja de
ser contable. Para eso está el
[Programa de Alianzas de MG Fiscal](https://mgfiscal.com.mx/alianzas.html):
tú sigues llevando a tu cliente.
