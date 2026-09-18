# Payments App — Groovy Music Store

Módulo de pagos de un marketplace de música física. Esta aplicación gestiona el ciclo de vida de los pagos: inicia el checkout con Mercado Pago, registra transacciones, administra la acreditación de fondos a vendedores y permite gestionar reembolsos y reclamos.

Forma parte de un ecosistema compuesto por cuatro aplicaciones independientes que se comunican mediante APIs.

## Rol dentro del sistema

La **Payments App** es responsable del dominio de pagos y se integra con:

* **Buyer App:** inicia los pagos y consulta el estado de las transacciones.
* **Seller App:** consulta balances y fondos acreditados.
* **Shipping App:** confirma la entrega para liberar los fondos al vendedor.
* **Control Plane:** permite administrar reembolsos, liberaciones y consultar métricas.

## Stack

**Next.js (App Router, TypeScript)** · **Prisma 6** · **PostgreSQL (Neon)** · **Clerk** · **Mercado Pago Checkout Pro (Sandbox)** · **Tailwind CSS** · **Vercel**

## Deploy

* **Payments App:** https://proyecto-c-payments-groovy-music-st.vercel.app/
* **Buyer App:** https://proyecto-c-buyer2-groovy-music-store.vercel.app/

El flujo de pago se inicia desde la **Buyer App** y continúa en el checkout de Mercado Pago utilizando el entorno Sandbox.

## Cómo probar

1. Ingresar a la **Buyer App**.
2. Seleccionar un producto y comenzar el proceso de compra.
3. Desde la Buyer App se inicia el checkout de Mercado Pago.
4. Completar el pago utilizando las credenciales de prueba del entorno Sandbox.
5. Volver a la aplicación y consultar el estado de la transacción.

### Acceso al panel de administración

<details>
<summary>Credenciales de prueba</summary>

Usuario: `adminpayments`
Contraseña: `adminpayments`

</details>

### Datos de prueba de Mercado Pago

<details>
<summary>Credenciales del comprador y tarjeta de prueba</summary>

**Comprador de test**

`TESTUSER7971489035181850335`

Código: `965242`

**Tarjeta**

* Número: `4002 7686 9439 5619`
* Nombre: `APRO`
* CVV: `123`
* Vencimiento: `11/30`
* DNI: `12345678`

</details>

## Endpoints

<details>
<summary>Endpoints consumidos por otras aplicaciones</summary>

### Buyer App

| Método y ruta                 | Para qué                                                  |
| ----------------------------- | --------------------------------------------------------- |
| `POST /api/payments/checkout` | Inicia el pago y devuelve el `init_point` de Mercado Pago |
| `GET /api/payments/:id`       | Consulta el estado de una transacción                     |

### Shipping App

| Método y ruta                              | Para qué                                            |
| ------------------------------------------ | --------------------------------------------------- |
| `POST /api/payments/delivery-confirmation` | Confirma la entrega y libera los fondos al vendedor |

### Seller App

| Método y ruta                   | Para qué                                                 |
| ------------------------------- | -------------------------------------------------------- |
| `GET /api/payouts?sellerId=:id` | Consulta el balance retenido y acreditado de un vendedor |

</details>

<details>
<summary>Endpoints consumidos por el Control Plane</summary>

| Método y ruta                              | Para qué                                     |
| ------------------------------------------ | -------------------------------------------- |
| `POST /api/payments/:id/refund`            | Gestiona reembolsos totales o parciales      |
| `POST /api/payments/:id/release`           | Libera fondos manualmente                    |
| `GET /api/payouts`                         | Lista los balances de los vendedores         |
| `GET /api/analytics/reclamos`              | Consulta métricas de reclamos                |
| `GET /api/analytics/resumen`               | Consulta un resumen general de transacciones |
| `GET /api/analytics/transacciones-por-dia` | Obtiene la serie de transacciones por día    |

</details>

<details>
<summary>Endpoint interno</summary>

| Método y ruta                | Para qué                                  |
| ---------------------------- | ----------------------------------------- |
| `POST /api/payments/webhook` | Recibe las notificaciones de Mercado Pago |

</details>

