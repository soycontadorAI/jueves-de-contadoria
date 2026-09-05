# Episodio 07 · Así piensa la IA que te va a auditar

Teoría de grafos para contadores. Qué es un nodo, qué es una arista, y por qué
un modelo que mira la red encuentra cosas que tú no ves aunque revises factura
por factura.

La idea del episodio en una línea: **tu cliente puede estar a dos pasos de una
empresa del 69-B sin haberle comprado nada.** Basta con que compartan
proveedor.

## Qué hay aquí

| Archivo | Qué es |
|---|---|
| [`prompt-analisis-de-red.md`](prompt-analisis-de-red.md) | El prompt de la clase, completo y listo para copiar. |
| [`datos/cfdi-demo-ficticio.csv`](datos/cfdi-demo-ficticio.csv) | La base de la demo: 95 facturas, 10 empresas, enero a junio 2026. |
| [`datos/lista-marcada-demo-ficticia.csv`](datos/lista-marcada-demo-ficticia.csv) | La lista de señalados, también de mentiras. Dos RFC. |
| [`mapa-de-la-red.svg`](mapa-de-la-red.svg) | El mapa ya dibujado, para que compares contra lo que te salga a ti. |

**Todo es inventado.** Las empresas se llaman como letras griegas a propósito,
para que a nadie se le ocurra que estoy señalando a una empresa de verdad.

## Cómo repetir el ejercicio

1. Abre Claude y sube los dos CSV de `datos/`.
2. Pega el prompt completo de `prompt-analisis-de-red.md`.
3. Compara lo que te devuelve contra la lista de abajo.

Cuando lo hagas con tu base real, exporta a **CSV y no a Excel**: pesa menos y
se procesa más limpio. Con emisor, receptor, fecha y monto ya tienes el mapa,
no necesitas treinta columnas. Y filtra por periodo o por cliente antes de
subir, que hay tope de tamaño por archivo.

Una cosa más, y va en serio: para practicar usa **estos datos o los tuyos
anonimizados**. El secreto profesional aplica igual cuando el que lee es un
modelo.

## Qué tiene que salir

Si el resultado no trae estas cinco cosas, el problema fue el prompt, no la
base. Vuelve a pedirlo.

1. **Ninguno de los tres clientes tiene relación directa** con un
   contribuyente de la lista.
2. **Muebles Alfa está a dos pasos de Constructora Omega.** El puente es
   Insumos Delta, que le vende a los dos. Alfa nunca le compró nada a Omega:
   no hay una sola operación entre ellos.
3. **Textiles Beta y Panificadora Gamma salen limpios.** Ni directo ni a dos
   pasos. Este es el resultado que más vale, y ahorita te digo por qué.
4. **Hay un ciclo:** Constructora Omega → Servicios Eta → Comercializadora
   Sigma → y de regreso a Omega. Un círculo. En la vida real, un círculo casi
   nunca es casualidad.
5. **El más conectado es Papelería Zeta**, que opera con cuatro empresas
   distintas.

Sobre el punto 3, que es el que la gente se salta: **si la herramienta te
dijera que los tres están conectados, no deberías creerle nada.** Que sepa
decir que no es exactamente lo que la vuelve útil.

## Los tres términos del episodio

- **Nodo:** un contribuyente. Un punto en el dibujo.
- **Arista:** una operación entre dos. La línea que los une.
- **Grafo:** el dibujo completo. Puntos y líneas, nada más.

Con esos tres ya entiendes la frase del Plan Nacional de Inteligencia
Artificial que leímos en clase, la que hablaba de subgrafos, comunidades,
ciclos y rutas de propagación de riesgo.

## La asimetría, que es lo incómodo

Tú ves el mapa de **tu** cliente: sus proveedores, sus clientes, sus facturas.
No tienes los del proveedor de su proveedor, ni por qué tendrías.

La autoridad ve el padrón completo. Ahí está la diferencia, y no se cierra con
esfuerzo ni con más horas: se cierra cambiando la pregunta que te haces cuando
das de alta a un proveedor nuevo. Ya no es solo "¿su CFDI está bien?". Es
también "¿a quién más le vende?".

## Descarga relacionada

**5 prompts para auditar tus XMLs con Claude**, gratis:
[soycontador.ai/audita](https://soycontador.ai/audita)
