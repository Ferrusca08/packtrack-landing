# PackTrack — Propuesta de precios

> Modelo de cobro: **por residente activo en la app, por mes.**
> Moneda: **MXN** (pesos mexicanos). Tipo de cambio de referencia: 1 USD ≈ 18 MXN.

---

## 1. Costo real de la app *as-is* (infraestructura AWS)

La app corre 100% serverless. El costo es casi todo **variable** (escala con el uso) y muy bajo gracias al free tier de AWS.

### Supuestos del modelo
- **3 paquetes / residente activo / mes** (promedio conservador).
- 1 lectura OCR (Rekognition) por paquete.
- 1 foto (~2 MB) por paquete en S3.
- Notificaciones **push** (gratis). SMS apagado por ahora.

### Costo por servicio (ejemplo: edificio de 100 residentes activos = ~300 paquetes/mes)

| Servicio AWS | Qué hace | Costo aprox. /mes |
|---|---|---|
| **Rekognition** (DetectText) | OCR de la etiqueta | 300 × $0.001 USD = **$0.30** |
| **Lambda** | Lógica de negocio | Free tier (1M req) → **$0** |
| **AppSync** (GraphQL) | API | ~Free tier → **~$0.05** |
| **DynamoDB** (on-demand) | Base de datos | **~$0.15** |
| **S3** | Fotos de etiqueta/evidencia | **~$0.50** |
| **Cognito** | Logins (50k MAU gratis) | **$0** |
| **SNS push** | Notificaciones | Free tier (1M) → **$0** |
| **CloudWatch / EventBridge / otros** | Logs, recordatorios | **~$1.50** |
| **TOTAL infraestructura** | | **≈ $2.5 – $4 USD/mes** |

> **≈ $45 – $72 MXN/mes para 100 residentes** → **≈ $0.45 – $0.72 MXN por residente activo.**

### Costo unitario aproximado

| Concepto | Costo |
|---|---|
| **Costo de infraestructura por residente activo/mes** | **≈ $0.50 – $1.50 MXN** |
| Costo marginal por paquete (OCR + storage) | ≈ $0.02 MXN |
| Si se activa **SMS** (≈ $0.40 MXN/SMS × 3) | + ≈ $1.20 MXN/residente |

**Conclusión:** la infraestructura es baratísima. El precio NO es costo-plus, es **basado en valor** — y deja un margen bruto >95%.

> ⚠️ Nota: este costo es **solo infraestructura**. El precio de venta también debe cubrir soporte, desarrollo continuo, comisiones de cobro (~3.6% + IVA con pasarelas mexicanas), impuestos y utilidad.

---

## 2. Modelo de precio — por residente activo

Precio escalonado por volumen (a más residentes, menor precio unitario):

| Residentes activos | Precio /residente/mes | Margen bruto* |
|---|---|---|
| 1 – 50 | **$29 MXN** | ~97% |
| 51 – 150 | **$24 MXN** | ~96% |
| 151 – 300 | **$19 MXN** | ~95% |
| 301 + | **$15 MXN** (o a medida) | ~93% |

\* Margen sobre costo de infraestructura. No incluye soporte/operación.

**Mínimo mensual: $990 MXN/mes** — hace viable atender edificios chicos (cubre soporte y operación base).

**Cuota de alta (opcional): $2,500 MXN única vez** — onboarding, carga de padrón y capacitación. Negociable / waivable en contratos anuales.

---

## 3. Planes comerciales (para la landing)

Los planes empaquetan el precio por residente + funciones, por tamaño de edificio:

### 🟦 Esencial — $29 MXN/residente/mes
**Edificios pequeños (hasta 50 residentes activos).** Mínimo $990/mes.
- App de guardia y residente
- Registro con foto + OCR (match por departamento)
- Notificaciones push
- Código de retiro seguro + historial
- 1 edificio · soporte por correo

### 🟪 Profesional — $22 MXN/residente/mes — *Más popular*
**Edificios medianos (51–200 residentes activos).**
- Todo lo de Esencial, más:
- Notificaciones por **SMS**
- Hasta 3 torres por edificio
- Reportes exportables
- Soporte prioritario

### ⬛ Premium — desde $15 MXN/residente/mes
**Conjuntos / multi-torre (200+ residentes activos).** Precio a medida.
- Todo lo de Profesional, más:
- Multi-edificio ilimitado
- Marca personalizada (white-label)
- Onboarding dedicado + SLA

---

## 4. Ejemplos de facturación

| Edificio | Residentes activos | Plan | Cálculo | **Mensual** | Costo AWS | **Utilidad bruta** |
|---|---|---|---|---|---|---|
| Pequeño | 40 | Esencial | máx(40×$29, mín $990) | **$1,160** | ~$30 | ~$1,130 |
| Mediano | 120 | Profesional | 120 × $22 | **$2,640** | ~$70 | ~$2,570 |
| Grande | 250 | Premium | 250 × $19 | **$4,750** | ~$140 | ~$4,610 |
| Conjunto | 600 | Premium | 600 × $15 | **$9,000** | ~$320 | ~$8,680 |

> Los costos AWS incluyen un margen de seguridad. La utilidad mostrada es **bruta** (antes de soporte, comisiones de cobro, impuestos y operación).

---

## 5. Recomendaciones

1. **Cobro anual con descuento** (ej. 2 meses gratis al pagar 12) para asegurar flujo y reducir churn.
2. **Prueba gratis de 30 días** para reducir fricción de entrada (el costo de infraestructura de una prueba es de centavos).
3. **SMS como add-on** del plan Profesional+ (su costo sí es real, ~$1.20 MXN/residente) — o incluirlo y subir levemente el precio del tier.
4. Revisar el **tipo de cambio USD/MXN** trimestralmente: el costo AWS se factura en USD.
5. Definir bien "**residente activo**" en el contrato (cuenta con sesión iniciada en el mes) para evitar disputas de facturación.

---

*Documento de referencia interna. Cifras de costo basadas en precios públicos de AWS (us-east-1) y los supuestos indicados. Ajustar con datos reales de consumo tras el primer mes en producción.*
