# Episodio 12 · Discrepancia fiscal: complementos de pago vs facturas vs estado de cuenta

Segundo episodio de la serie **«Cuando el algoritmo ya te señaló»**. Serie
presentada por Certera.

Una factura PPD se emite hoy y se cobra después. Entre una cosa y la otra
viven tres registros en tres lugares: la factura y el complemento de pago en
el SAT, y el depósito en el banco. Cuando no cuadran entre sí, alguien los
tiene que juntar. Mejor que seas tú antes que el SAT.

Hoy el material no es un prompt: es una **skill**. Un prompt lo pegas cada
vez; una skill se instala una vez y Claude la usa sola cuando le subes los
archivos.

## Qué hay aquí

| Archivo | Qué es |
|---|---|
| [`conciliacion-pagos.zip`](conciliacion-pagos.zip) | **La skill, lista para subir a Claude.** Descárgala tal cual. |
| [`conciliacion-pagos/SKILL.md`](conciliacion-pagos/SKILL.md) | La misma skill en texto, para leerla o modificarla. |
| [`datos/facturas-ficticio.csv`](datos/facturas-ficticio.csv) | Seis facturas emitidas de julio a septiembre de 2026, cinco PPD y una PUE. |
| [`datos/complementos-de-pago-ficticio.csv`](datos/complementos-de-pago-ficticio.csv) | Los complementos de pago que se emitieron. |
| [`datos/estado-de-cuenta-ficticio.csv`](datos/estado-de-cuenta-ficticio.csv) | Los depósitos del banco hasta el 7 de octubre. |

**Todo es inventado.** El contribuyente es una persona física con actividad
empresarial que no existe, y los clientes se llaman Alfa, Beta, Gamma, Delta,
Epsilon y Zeta a propósito.

## Cómo instalarla

1. Descarga [`conciliacion-pagos.zip`](conciliacion-pagos.zip). No lo
   descomprimas.
2. En Claude: **Configuración → Capacidades → Skills → Subir skill**, y elige
   el .zip. Actívala.
3. La ruta del menú cambia seguido y no en todos los planes hay skills. Si no
   la encuentras, busca «Skills» en la configuración de tu cuenta.

## Cómo repetir el ejercicio

1. Abre un chat (de preferencia dentro de un proyecto de Claude) con la skill
   activa.
2. Sube los tres CSV de `datos/`.
3. Escribe:

```
Concilia los pagos de septiembre.
```

Si no la usa sola, pídeselo por nombre: «usa la skill conciliacion-pagos».

Con tus datos reales, primero decide con qué cuenta van (el episodio del 24
de septiembre, «¿Qué hace la IA con tus datos?», es justo eso), y prueba la
skill con estos datos antes de usar los de un cliente.

## Qué tiene que salir

Si el resultado no trae esto, vuelve a pedirlo antes de dudar de la skill.
Un caso sembrado por factura:

| Factura | Qué pasa | Grupo |
|---|---|---|
| Alfa, PPD 58,000 | Dos parcialidades de 29,000, con complemento y en el banco. El saldo llega a 0 | EN ORDEN |
| Zeta, PPD 11,600 | Sin complemento y sin depósito | POR COBRAR |
| Beta, PPD 34,800 | Depósito de 34,800 el 5 de septiembre, sin complemento | EMITIR COMPLEMENTO |
| Gamma, PPD 23,200 | Complemento por 23,200, sin depósito en esta cuenta | ACLARAR CON CLIENTE |
| Delta, PPD 46,400 | Complemento por 40,000, pero al banco llegaron 46,400 | CORREGIR COMPLEMENTO |
| Epsilon, PUE 17,400 | Emitida el 8 de septiembre, cobrada el 6 de octubre | REVISAR MÉTODO DE PAGO |

Totales:

| Concepto | Monto |
|---|---|
| Facturado (6 facturas, con IVA) | 191,400 |
| Amparado por complementos | 121,200 |
| Depositado (5 movimientos) | 156,600 |
| Depositado sin complemento | 41,200 |
| Complementado sin depósito | 23,200 |

Alfa es el control: si la skill la marca, está mal.

## Lo que esta skill sí hace y lo que no

Cruza, clasifica y te dice qué le preguntarías al cliente. **No emite, no
cancela ni corrige CFDI**, no calcula impuesto a cargo y no decide por ti qué
se corrige: eso, y la firma, siguen siendo tuyos.
