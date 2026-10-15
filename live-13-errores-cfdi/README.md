# Episodio 13 · Errores de CFDI: lo emitido vs lo registrado, y la fecha de operación

Tercer episodio de la serie **"Cuando el algoritmo ya te señaló"**. Serie
presentada por Certera.

El SAT no lee tu sistema contable: lee tus CFDI. Si lo que timbraste y lo que
registraste no cuentan la misma historia, la que él cree es la de los CFDI.
Hoy se cruzan los dos por UUID, factura por factura, y de paso se separa la
fecha de emisión de la fecha de la operación.

En la clase va como **prompt**, para ver las reglas una por una. Si lo vas a
correr cada mes, conviene instalarlo como **skill**, como la del
[episodio 12](../live-12-discrepancia-fiscal/): las mismas reglas, y se
instala una sola vez.

## Qué hay aquí

| Archivo | Qué es |
|---|---|
| [`prompt-revision-de-lote.md`](prompt-revision-de-lote.md) | El prompt de la clase, para pegarlo en el proyecto del cliente. |
| [`revision-de-lote.zip`](revision-de-lote.zip) | **La skill, lista para subir a Claude.** Descárgala tal cual. |
| [`revision-de-lote/SKILL.md`](revision-de-lote/SKILL.md) | La misma skill en texto, para leerla o modificarla. |
| [`datos/cfdi-emitidos-ficticio.csv`](datos/cfdi-emitidos-ficticio.csv) | Siete CFDI emitidos en septiembre de 2026, con estatus y relaciones. |
| [`datos/cfdi-recibidos-ficticio.csv`](datos/cfdi-recibidos-ficticio.csv) | Cuatro CFDI recibidos, hasta el 3 de octubre. |
| [`datos/registro-contable-ficticio.csv`](datos/registro-contable-ficticio.csv) | Las pólizas del sistema, cada una con su UUID. |

**Todo es inventado.** La comercializadora no existe, y los clientes se llaman
Alfa, Beta, Gamma, Delta, Epsilon y Zeta a propósito. Ojo: son otros casos
que los del episodio 12, aunque se llamen igual.

## La skill

1. Descarga [`revision-de-lote.zip`](revision-de-lote.zip). No lo descomprimas.
2. En Claude: **Configuración → Capacidades → Skills → Subir skill** (en
   español puede decir "Habilidades"), y elige el .zip. Actívala.
3. La ruta del menú cambia seguido y no en todos los planes hay skills. Si no
   la encuentras, busca "Skills" en la configuración de tu cuenta.

## Cómo repetir el ejercicio

1. Abre un chat (de preferencia dentro de un proyecto de Claude) con la skill
   activa, o pega el prompt.
2. Sube los tres CSV de `datos/`.
3. Escribe:

```
Revisa el lote de septiembre.
```

Si no la usa sola, pídeselo por nombre: "usa la skill revision-de-lote".

Con tus datos reales, primero decide con qué cuenta van (el episodio del 24
de septiembre, "¿Qué hace la IA con tus datos?", es justo eso), y prueba con
estos datos antes de usar los de un cliente.

## Qué tiene que salir

Si el resultado no trae esto, vuelve a pedirlo antes de dudar del prompt.
Ingresos de septiembre, sin IVA:

| | Monto |
|---|---|
| Según el SAT (emitidos vigentes, subtotal menos descuento) | 63,500 |
| Según el sistema (cuenta 401 neta) | 93,500 |
| Diferencia | 30,000 |

Y los seis hallazgos que la explican completa:

| Caso | Qué pasa | Efecto |
|---|---|---|
| Beta, 8,000 | Timbrada y no registrada | −8,000 |
| Gamma | Dedazo: 12,000 capturados como 21,000 | +9,000 |
| Delta, 5,000 | Cancelada el 20 de septiembre, viva en el sistema | +5,000 |
| Epsilon, 20,000 | Sustitución (relación 04) registrada dos veces | +20,000 |
| Venta mostrador Zeta | Póliza de ingreso sin UUID | +6,000 |
| Proveedor Uno | Nota de crédito recibida restada de ventas | −2,000 |

Del lado de gastos: la renta de septiembre se facturó el 3 de octubre y el
sistema la tiene en octubre. Por fecha de operación, y con el descuento ya
restado de compras, septiembre tiene 44,000 de gasto y no 28,000.

Las dos facturas de Alfa son el control: si las marca, está mal. La segunda
trae su propio descuento y la póliza lo registra bien.

## Lo que esto sí hace y lo que no

Cruza, clasifica y te dice qué le preguntarías al cliente. **No emite, no
cancela ni corrige CFDI ni pólizas**, no calcula impuesto a cargo y no decide
por ti qué se corrige: eso, y la firma, siguen siendo tuyos.
