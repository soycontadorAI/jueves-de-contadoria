# Prompt: análisis de red sobre tu base de CFDI

El de la clase, tal cual. Súbele los dos CSV de `datos/` y pégalo completo.

Si lo vas a usar con tu propia base, cambia nada más el bloque de **contexto**:
los nombres y RFC de tus clientes. Lo demás funciona igual.

---

```
## [ R · ROL ]

Eres analista de riesgo fiscal. Trabajas para un despacho contable en
México y tu trabajo es mirar la RED de relaciones entre contribuyentes,
no las facturas una por una.

## [ C · CONTEXTO ]

Te adjunto dos archivos:

1. Una base de CFDI de un periodo. Cada renglón es una operación entre
   dos contribuyentes: quién emitió y quién recibió.
2. Una lista de contribuyentes señalados por la autoridad.

Los clientes de mi despacho son:
- MUEBLES ALFA SA DE CV (MAL950101AB1)
- TEXTILES BETA SA DE CV (TBE980215CD2)
- PANIFICADORA GAMMA SA DE CV (PGA020310EF3)

Los demás RFC del archivo son terceros: proveedores, o empresas que
aparecen porque operan con mis proveedores.

## [ I · INSTRUCCIÓN ]

Analiza los archivos ESCRIBIENDO CÓDIGO, no leyéndolos a ojo. Quiero
resultados reproducibles, no impresiones.

Trata cada RFC como un nodo y cada operación como una conexión
dirigida (emisor → receptor). Con eso:

1. Dime cuántos contribuyentes distintos y cuántas conexiones únicas
   hay en total.
2. Para CADA UNO de mis tres clientes, revisa si tiene operación
   DIRECTA con algún contribuyente de la lista de señalados. Dilo
   explícitamente, incluso cuando la respuesta sea que no.
3. Para CADA UNO de mis tres clientes, busca conexiones INDIRECTAS a
   dos pasos con la lista de señalados: casos donde mi cliente y un
   señalado comparten un mismo tercero (un proveedor en común, o un
   cliente en común). Muéstrame la cadena completa con nombres y RFC.
4. Busca ciclos: cadenas de operaciones que salgan de un contribuyente,
   pasen por otros y regresen al mismo. Si encuentras alguno,
   dibújamelo como secuencia.
5. Dime qué contribuyente es el más conectado del archivo (con cuántos
   opera) y por qué eso importa.

## [ F · FORMATO ]

Una sección por punto. Para las conexiones indirectas, una tabla con:
cliente | tercero en común | contribuyente señalado | situación |
no. de operaciones | monto involucrado.

Al final, un apartado "QUÉ DEBO VERIFICAR" con lo que a mí me toca
confirmar a mano.

## [ RESTRICCIONES ]

1. Si un RFC no aparece en los archivos, NO lo infieras ni lo
   completes. Dime que no está.
2. NO concluyas que una conexión indirecta implica irregularidad.
   Descríbela como lo que es: una relación que amerita revisión.
3. Si un cliente NO tiene conexiones, dilo con todas sus letras. No
   fuerces un hallazgo para darme la razón.
4. Muéstrame el código que usaste. Quiero poder auditarlo.
```

---

## Las dos líneas que más importan

Si te vas a llevar algo de este prompt, que sean estas dos.

**"Analiza escribiendo código, no leyéndolo a ojo."** Aquí son 95 renglones y
sí se podrían leer. Con tu base real, no. Y un análisis programado se puede
repetir el mes que entra y da lo mismo; una lectura a ojo es una impresión, y
las impresiones cambian según el día que traigas.

**"Si un cliente NO tiene conexiones, dilo con todas sus letras."** Esta es la
que casi nadie pone y la que más vale. Tú vas a llegar preguntando si tus
clientes están conectados con empresas marcadas, o sea que ya llegas
esperando un sí. Sin esta línea, el modelo te arma una cadena preciosa que no
existe con tal de darte la razón. Una conexión inventada es peor que no haber
hecho el ejercicio.

## Si quieres pedirle además el dibujo

Agrégale esto al bloque de formato:

```
Dibújame también la red completa como diagrama: un círculo por empresa,
una flecha por cada relación de facturación, mis clientes en azul, los
señalados en rojo, y resaltada la cadena que encontraste.
```

Una tabla no es una red. En `mapa-de-la-red.svg` está el mismo mapa dibujado,
por si quieres comparar contra lo que te devuelva a ti.
