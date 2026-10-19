# Primer Estudio de Caso — Análisis de Expresiones Aritméticas con Pilas (LIFO)

**Curso:** Estructuras de Datos (SOFT-10) — Universidad CENFOTEC
**Tema seleccionado:** Análisis de expresiones aritméticas
**Tokens contemplados:** números literales, variables numéricas, operadores (+, -, *, /) y paréntesis.

---

## 1. Estructura de carpetas del proyecto

```
PrimerEstudioDeCaso_SOFT10/
│
├── 01_Documento/                          ← PARTE TEÓRICA (documento académico)
│   ├── PrimerEstudioDeCaso_AnalisisExpresiones.pdf    (versión lista para entregar)
│   └── PrimerEstudioDeCaso_AnalisisExpresiones.md     (fuente editable del documento)
│
├── 02_CodigoFuente/                       ← PARTE PRÁCTICA (código Java)
│   └── src/
│       └── com/
│           └── cenfotec/
│               └── soft10/
│                   └── estudiocaso/
│                       ├── Token.java                  (Clase 1: token + nodo)
│                       ├── Pila.java                   (Clase 2: pila enlazada LIFO)
│                       ├── AnalizadorAritmetico.java   (Clase 3: tokenización,
│                       │                                    balanceo, Shunting-yard,
│                       │                                    evaluación postfija)
│                       └── Main.java                   (Clase 4: menú interactivo)
│
└── README.md                              ← ESTE ARCHIVO (guía del proyecto)
```

> **Regla del paquete Java:** como las clases usan el paquete
> `com.cenfotec.soft10.estudiocaso`, la ruta de carpetas debe coincidir
> exactamente con el nombre del paquete (`src/com/cenfotec/soft10/estudiocaso`).

---

## 2. Cómo compilar y ejecutar

### Opción A — Línea de comandos (javac / java)

Desde la carpeta `02_CodigoFuente/`:

```bash
# Compilar (los .class se guardan en la carpeta bin)
javac -d bin src/com/cenfotec/soft10/estudiocaso/*.java

# Ejecutar
java -cp bin com.cenfotec.soft10.estudiocaso.Main
```

### Opción B — IntelliJ IDEA / Eclipse / NetBeans

1. `File → New Project from Existing Sources` y seleccione la carpeta `02_CodigoFuente`.
2. Marque `src` como *Sources Root*.
3. Ejecute la clase `Main` (clic derecho → Run).

---

## 3. Contenido del menú de la aplicación

| Opción | Descripción |
|:------:|-------------|
| 1 | Ingresar y analizar una expresión aritmética (tokeniza, valida balanceo, convierte a postfijo y permite evaluar) |
| 2 | Ver el estado de la pila paso a paso del último análisis (registro de PUSH/POP) |
| 3 | Probar operaciones fundamentales de la pila manualmente (Push, Pop, Peek, imprimir) |
| 4 | Salir |

---

## 4. Casos de prueba sugeridos para la defensa

| Entrada | Resultado esperado |
|---------|--------------------|
| `a + (b * 5)` | Balanceada ✅ · Postfijo: `a b 5 * +` |
| `a + (b * 5` | NO balanceada: falta `)` |
| `(a + b)) * 2` | NO balanceada: `)` sin apertura |
| `10 + 20 * 3` | Balanceada · Postfijo: `10 20 3 * +` · Valor: 70 |
| `((x + 2) * (y - 3))` | Balanceada · Postfijo: `x 2 + y 3 - *` |

---

## 5. Descripción de las clases

| Clase | Responsabilidad |
|-------|-----------------|
| `Token` | Representa un token léxico (NÚMERO, VARIABLE, OPERADOR, PARÉNTESIS_IZQ, PARÉNTESIS_DER) y funciona simultáneamente como nodo de la pila enlazada (puntero `siguiente`). |
| `Pila` | Implementación propia de pila LIFO con nodos enlazados: `push`, `pop`, `peek`, `estaVacia`, `getTamaño`, `imprimirPila`. Sin usar `java.util.Stack`. |
| `AnalizadorAritmetico` | Lógica del caso: tokenización, validación de balanceo con pila, conversión infija→postfija (Shunting-yard) y evaluación postfija con valores de variables. |
| `Main` | Menú interactivo por consola (Scanner) con las 4 opciones y validación de entradas. |
