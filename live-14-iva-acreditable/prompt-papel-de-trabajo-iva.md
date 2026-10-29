# El papel de trabajo del IVA acreditable, antes de pedir la devolución

Jueves de ContadorIA · 22 de octubre de 2026 · Serie "Cuando el algoritmo ya te señaló"
Serie presentada por Certera.

Dos piezas: las **instrucciones del proyecto** (una vez por cliente) y el
**prompt** (cada mes, y sin falta antes de pedir una devolución). Al final, un
ejemplo del papel de trabajo que sale.

---

## 1. Instrucciones del proyecto

Si ya armaste el proyecto del cliente con la conciliación del 1 de octubre,
úsalo: las reglas son las mismas. Si no, crea uno por cliente y pega esto en
"Instrucciones del proyecto":

```
Eres mi auxiliar de revisión fiscal. Trabajas para un contador público en
México. El contribuyente de este proyecto es [persona moral / persona física
con actividad empresarial], RFC [RFC].

Reglas que no se rompen:
1. Solo usas los archivos que te doy. Si falta un dato, lo dices; no lo supones.
2. Los montos se escriben con dos decimales y se suman en pesos mexicanos.
3. Una diferencia no es un error hasta que se revisa. La clasificas, no la juzgas.
4. Cuando cites una disposición fiscal, di ley, artículo y fracción. Si no
   estás seguro del artículo, dilo en vez de inventarlo.
5. La decisión y la firma son del contador. Tú preparas el papel de trabajo.
```

## 2. El prompt

Sube al chat del proyecto: los CFDI recibidos del periodo (el Excel de la
descarga masiva), lo que muestra hoy el portal del SAT para esos CFDI, el
estado de cuenta, la lista 69-B vigente y lo que declaraste. Después:

```
Arma el papel de trabajo del IVA acreditable de [periodo]. Voy a pedir la
devolución del saldo a favor y quiero saber cuánto resiste una revisión.

Cruza tres fuentes por UUID:
- Lo que llegó: los CFDI recibidos.
- Lo que ve el SAT hoy: el estatus y el IVA del portal. Si un CFDI está
  cancelado hoy, cuenta como cancelado aunque estuviera vigente al descargar.
- Lo que pagaste: el estado de cuenta. Relaciona cada CFDI con su pago por
  monto, fecha y proveedor. Si no encuentras el pago, dilo.

Clasifica cada CFDI en UNO de estos grupos, con el motivo en una línea:
- ACREDITABLE: vigente hoy, pagado, forma de pago que no rebasa el tope de
  efectivo, proveedor fuera del 69-B y gasto del negocio.
- NO ACREDITABLE ESTE MES: PPD sin complemento o sin pago. Se acredita cuando
  se pague.
- NO ACREDITABLE: cancelado, proveedor en 69-B definitivo, pagado en efectivo
  arriba del tope.
- REVISAR: lo que parezca no deducible por el concepto o la forma de pago.
  No lo decides tú; dime qué le preguntarías al cliente.

Entrégame:
1. La tabla por CFDI: UUID corto, proveedor, IVA, pago encontrado (fecha y
   monto), estatus hoy, grupo y motivo.
2. El resumen: IVA de lo que llegó, IVA que muestra el portal, IVA declarado,
   IVA acreditable según esta revisión, y el saldo a favor que resulta con el
   IVA trasladado que te doy.
3. La diferencia contra lo declarado, desglosada renglón por renglón, que
   sume exacto.
4. Qué se corrige (complementaria) y qué se espera al mes siguiente.

No afirmes requisitos legales que no puedas citar con precisión. Si un
criterio depende de la interpretación, márcalo como REVISAR.
```

## 3. Ejemplo del papel de trabajo que sale

Con los datos ficticios del live (comercializadora de prueba, septiembre de
2026):

| UUID | Proveedor | IVA | Pago | Estatus hoy | Grupo | Motivo |
|---|---|---|---|---|---|---|
| …0001 | Proveedor Uno | 16,000.00 | 05-sep, 116,000.00 | Vigente | ACREDITABLE | Pagado por transferencia |
| …0002 | Proveedor Dos | 8,000.00 | 12-sep, 58,000.00 | Vigente | ACREDITABLE | Pagado por transferencia |
| …0003 | Proveedor Tres | 12,800.00 | No encontrado | Vigente | NO ACREDITABLE ESTE MES | PPD sin complemento ni pago |
| …0004 | Proveedor Cuatro | 4,800.00 | 18-sep, 34,800.00 | Vigente | NO ACREDITABLE | Proveedor en 69-B definitivo |
| …0005 | Proveedor Cinco | 3,200.00 | 20-sep, 23,200.00 | Cancelado | NO ACREDITABLE | El proveedor la canceló |
| …0006 | Restaurante | 800.00 | No sale del banco de la empresa | Vigente | REVISAR | Fin de semana del socio |
| …0007 | Proveedor Siete | 480.00 | Retiro en efectivo 22-sep | Vigente | NO ACREDITABLE | Efectivo arriba del tope |
| …0008 | Proveedor Ocho | 6,400.00 | 25-sep, 46,400.00 | Vigente | ACREDITABLE | Pagado; **no estaba declarado** |

| Resumen | IVA |
|---|---|
| Lo que llegó | 52,480.00 |
| Lo que muestra el portal | 49,280.00 |
| Lo declarado | 46,080.00 |
| **Acreditable según la revisión** | **30,400.00** |
| IVA trasladado cobrado | 20,000.00 |
| Saldo a favor declarado | 26,080.00 |
| **Saldo a favor que resiste** | **10,400.00** |

Diferencia contra lo declarado: 12,800 + 4,800 + 3,200 + 800 + 480 − 6,400 =
**15,680.00**.

## Por qué funciona

Pedir una devolución es pedirle al SAT que revise. Él cruza tus CFDI, su
propio portal, lo que el banco le informa y su lista 69-B. Este papel de
trabajo hace el mismo cruce antes, y te deja pedir solo lo que resiste.

## Antes de usarlo con datos reales

Pruébalo con datos ficticios, dentro de la cuenta correcta (jueves del 24 de
septiembre, "¿Qué hace la IA con tus datos?"). Y la clasificación final es
tuya: Claude prepara el papel, tú firmas.
