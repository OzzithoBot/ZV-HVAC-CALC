# HVAC Calculator — Documentación Técnica
## ZV PERU SAC

---

## 1. Carga Térmica (ASHRAE RTS Simplificado)

### 1.1 Metodología

Se utiliza el método simplificado ASHRAE RTS (Radiant Time Series) para el cálculo de carga térmica por componentes.

### 1.2 Fórmulas

#### Conducción a través de muros y techo
```
Q = U × A × ΔT
```
Donde:
- **U** = Coeficiente global de transferencia de calor (W/m²·K)
- **A** = Área de la superficie (m²)
- **ΔT** = Diferencia de temperatura (°C)
- Para techo: ΔT = (Tbs_ext + 5) - Tbs_int (considera radiación solar)

#### Ganancia solar por ventanas
```
Q_solar = A_vent × SHGC × 700 × 0.8
```
Donde:
- **SHGC** = Solar Heat Gain Coefficient (0-1)
- **700** = Radiación solar promedio (W/m²) para latitudes tropicales
- **0.8** = Factor de sombreado interior

#### Carga por ocupantes
```
Q_sensible = N × 75 W/persona
Q_latente = N × 55 W/persona
```
Valores según ASHRAE 55 para actividad ligera (oficina).

#### Carga por iluminación y equipos
```
Q_luz = A × W_luz (W/m²)
Q_eq = A × W_eq (W/m²)
```

#### Carga por ventilación
```
CFM = ACH × V / 0.0283168
Q_sensible = 1.23 × CFM × ΔT
Q_latente = 3010 × CFM × ΔW
```
Donde:
- **ACH** = Cambios de aire por hora
- **V** = Volumen del ambiente (m³)
- **ΔW** = Diferencia de humedad absoluta (kg/kg)

#### Carga por infiltración
```
CFM_inf = ACH_inf × V / 0.0283168
Q_sensible = 1.23 × CFM_inf × ΔT
```

### 1.3 Conversión a TR
```
TR = Q_total(W) × 3.412 / 12000
```

### 1.4 Valores de referencia U

| Elemento | U (W/m²·K) |
|----------|-------------|
| Muro ladrillo sin aislar | 2.0 - 3.0 |
| Muro con aislante | 0.5 - 1.0 |
| Techo sin aislar | 1.5 - 2.5 |
| Techo con aislante | 0.3 - 0.6 |
| Vidrio simple | 5.8 |
| Vidrio doble | 2.8 - 3.5 |

### 1.5 Fuentes
- ASHRAE Handbook — Fundamentals (2021), Cap. 17-18
- ASHRAE Standard 55 — Thermal Environmental Conditions
- ASHRAE Standard 62.1 — Ventilation

---

## 2. Selección de Equipos

### 2.1 Cálculo de TR
```
TR = Q_total(BTU/h) / 12000
```

### 2.2 Cálculo de CFM
```
CFM = Q_sensible / (1.08 × ΔT)
```
Donde ΔT = 12°F (diferencia típica de temperatura de suministro)

### 2.3 Sensible Heat Ratio (SHR)
```
SHR = Q_sensible / Q_total
```

### 2.4 Potencia eléctrica
```
P(W) = Q_total(BTU/h) / COP
```

### 2.5 Rangos de equipos por tipo

| Tipo | Rango TR | COP típico |
|------|----------|------------|
| Split pared | 0.5 - 3.0 | 3.0 - 4.0 |
| Fan Coil + Chiller | 2 - 50 | 3.5 - 5.0 |
| Paquete Rooftop | 3 - 100 | 2.8 - 3.5 |
| VRF | 2 - 200 | 4.0 - 6.0 |
| Chiller + AHU | 10 - 500+ | 4.0 - 6.0 |

### 2.6 Fuentes
- ASHRAE Handbook — HVAC Systems and Equipment (2020), Cap. 1-5
- ARI Standard 210/240 — Unitary Air-Conditioning Equipment

---

## 3. Tuberías de Refrigerante

### 3.1 Dimensionamiento por tablas

Los diámetros se seleccionan según tablas de capacidad ASHRAE/ARI para cada refrigerante:

#### Línea de líquido (diámetro en pulgadas)
| TR | R-410A | R-32 | R-22 |
|----|--------|------|------|
| 0.5 | 3/8 | 3/8 | 3/8 |
| 1.0 | 3/8 | 3/8 | 3/8 |
| 1.5 | 3/8 | 3/8 | 3/8 |
| 2.0 | 1/2 | 1/2 | 1/2 |
| 3.0 | 1/2 | 1/2 | 1/2 |
| 5.0 | 5/8 | 5/8 | 5/8 |
| 10.0 | 3/4 | 3/4 | 3/4 |
| 15.0 | 3/4 | 3/4 | 3/4 |
| 20.0 | 7/8 | 7/8 | 7/8 |

#### Línea de succión (diámetro en pulgadas)
| TR | R-410A | R-32 | R-22 |
|----|--------|------|------|
| 0.5 | 5/8 | 5/8 | 5/8 |
| 1.0 | 3/4 | 3/4 | 3/4 |
| 1.5 | 3/4 | 3/4 | 3/4 |
| 2.0 | 7/8 | 7/8 | 7/8 |
| 3.0 | 7/8 | 7/8 | 7/8 |
| 5.0 | 1-1/8 | 1-1/8 | 1-1/8 |
| 10.0 | 1-3/8 | 1-3/8 | 1-3/8 |
| 15.0 | 1-5/8 | 1-5/8 | 1-5/8 |
| 20.0 | 1-5/8 | 1-5/8 | 1-5/8 |

### 3.2 Longitud equivalente
```
L_eq = L_real + (N_accesorios × 1.5m) + Desnivel
```

### 3.3 Caída de presión estimada
```
ΔP_líquido = L_eq × 0.0328 × 2.5 (psi)
ΔP_succión = L_eq × 0.0328 × 1.5 (psi)
```

### 3.4 Criterios de diseño
- ΔP succión máxima: 3 psi (≈2°F de pérdida de saturación)
- Velocidad mínima succión: 1000 FPM (retorno de aceite)
- Velocidad máxima succión: 3000 FPM
- Velocidad línea líquido: 1-3 m/s

### 3.5 Fuentes
- ASHRAE Handbook — Refrigeration (2022), Cap. 1
- ASHRAE Handbook — HVAC Systems (2020), Cap. 6
- DuPont/Chemours Technical Bulletin — Refrigerant piping

---

## 4. Ductos (Altshul-Tsal + Huebscher)

### 4.1 Ecuación de Altshul-Tsal (pérdida de fricción)

```
Hf = 0.109136 × Q^1.9 / D^5.02
```
Donde:
- **Hf** = Pérdida de fricción (in.wg / 100 ft)
- **Q** = Caudal (CFM)
- **D** = Diámetro equivalente (pulgadas)

### 4.2 Ecuación de Huebscher (diámetro equivalente rectangular)

```
De = 1.30 × (a × b)^0.625 / (a + b)^0.25
```
Donde:
- **De** = Diámetro equivalente circular (pulgadas)
- **a** = Ancho del ducto rectangular (pulgadas)
- **b** = Alto del ducto rectangular (pulgadas)

### 4.3 Velocidad del aire
```
V = 183.346 × Q / D²
```
Donde:
- **V** = Velocidad (FPM)
- **Q** = Caudal (CFM)
- **D** = Diámetro (pulgadas)

### 4.4 Pérdida de presión total
```
ΔP_total = Hf × L / 100
```
Donde **L** = Longitud del tramo (ft)

### 4.5 Peso del ducto (galvanizado)
```
Perímetro = 2 × (a + b) / 12 (ft)  [rectangular]
Perímetro = π × D / 12 (ft)       [circular]
Peso = Perímetro × L × 1.5 (kg)
```
Factor 1.5 kg/m² para calibre 26 (estándar)

### 4.6 Velocidades recomendadas (SMACNA)

| Ubicación | V (FPM) |
|-----------|---------|
| Ducto principal | 1200 - 2000 |
| Ducto secundario | 800 - 1500 |
| Ramal | 600 - 1000 |
| Cuello difusor | 300 - 600 |

### 4.7 Resolución del sistema

El calculador resuelve el sistema iterativamente:
1. Si se dan Q y V → calcula D por continuidad
2. Si se dan Q y Hf → calcula D por Altshul-Tsal (Newton-Raphson)
3. Si se da D y un lado rectangular → calcula el otro por Huebscher (Newton-Raphson)

### 4.8 Fuentes
- Altshul, A.D. & Zhalilov, R.M. (1966) — "Hydraulic friction in heating and ventilation systems"
- Huebscher, R.G. (1948) — "Friction equivalents for round, rectangular and oval ducts"
- ASHRAE Handbook — Fundamentals (2021), Cap. 21 — Duct Design
- SMACNA — HVAC Duct Construction Standards (2005)

---

## 5. Difusores y Rejillas

### 5.1 Cálculo de cantidad
```
N_difusores = CFM_total / CFM_por_difusor
N_rejillas = CFM_total / CFM_por_rejilla
```

### 5.2 Velocidad de descarga
```
A_dif = tamaño² × 0.00064516 (m²)
V_descarga = CFM / A_dif (FPM)
```

### 5.3 Criterios de diseño
- Velocidad de descarga máxima: 600 FPM (confort)
- Velocidad de descarga mínima: 150 FPM (mezcla adecuada)
- Relación de aspecto difusor: 1:1 a 1:4
- Área efectiva = 70-85% del área nominal

### 5.4 Fuentes
- ASHRAE Handbook — Fundamentals (2021), Cap. 20 — Room Air Diffusion
- Titus Engineering Guidelines — Diffuser Selection
- Price Industries — Engineering Catalog

---

## 6. Tuberías de Agua Helada

### 6.1 Cálculo de diámetro

#### Caudal másico
```
Q(L/s) = GPM × 0.06309
Q(m³/s) = Q(L/s) / 1000
```

#### Área requerida
```
A_req = Q / V_max
```

#### Diámetro requerido
```
D_req = √(4 × A_req / π) × 1000 (mm)
```

#### Diámetro comercial seleccionado
Se selecciona el diámetro comercial inmediatamente superior de la serie: 20, 25, 32, 40, 50, 65, 80, 100, 125, 150, 200, 250, 300 mm

### 6.2 Velocidad real
```
A_com = π × (D_com/2000)²
V_real = Q / A_com
```

### 6.3 Caída de presión (Darcy-Weisbach simplificado)
```
L_eq = L + N_acc × 3 (m equivalentes)
ΔP = f × (L_eq/D) × (ρV²/2) / 9806.65 (m.ca)
```
Con f = 0.02 (factor de fricción típico para acero comercial)

### 6.4 Criterios de diseño
- Velocidad máxima: 1.2 m/s (sistemas pequeños) a 3.0 m/s (sistemas grandes)
- GPM por TR: 2.4 - 3.0 GPM/TR (ΔT = 10-12°F)
- ΔP máxima: 40 ft.ca/100ft (≈120 m.ca/100m)

### 6.5 Fuentes
- ASHRAE Handbook — HVAC Systems (2020), Cap. 12 — Hydronic Systems
- ASHRAE Handbook — Fundamentals (2021), Cap. 22 — Pipe Design
- Crane Technical Paper 410 — Flow of Fluids

---

## 7. Sistema Eléctrico

### 7.1 Potencia del equipo
```
P(W) = TR × 3517 / COP
```

### 7.2 Corriente nominal

#### Monofásico (220V)
```
I = P / (V × FP)
```

#### Trifásico (380V)
```
I = P / (V × √3 × FP)
```
Donde FP = 0.85 (factor de potencia típico)

### 7.3 Sección del cable
```
ΔV = V × (%ΔV/100)
S = (2 × ρ × L × I) / ΔV
```
Donde:
- **ρ** = 0.0172 Ω·mm²/m (cobre)
- **L** = Longitud del cable (m)
- **ΔV** = Caída de tensión admisible (V)

### 7.4 Selección de cable
Se selecciona la sección comercial inmediatamente superior de la serie: 2.5, 4, 6, 10, 16, 25, 35, 50, 70, 95, 120, 150, 185, 240 mm²

### 7.5 Protección (breaker)
```
I_breaker = I_nominal × 1.25
```
Se selecciona el breaker comercial inmediatamente superior.

### 7.6 Criterios según NEC/NTE E.020
- Caída de tensión máxima: 3% (alimentadores), 5% (total)
- Factor de sobrecarga: 125% para cargas continuas
- Conductores de cobre THW o THHN en conduit

### 7.7 Fuentes
- NEC (NFPA 70) — National Electrical Code, Art. 310, 210, 430
- NTE E.020 — Instalaciones eléctricas en edificios (Perú)
- ASHRAE Handbook — HVAC Systems (2020), Cap. 38 — Electrical Systems

---

## 8. Tablas de Metrado

### 8.1 Metrado de Ductos
La tabla de metrado de ductos calcula automáticamente:
- Peso unitario por tramo: `Perímetro × Longitud × 1.5 kg/m²`
- Peso total por ítem: `Peso unitario × Cantidad`
- Suma total de peso de ductos

### 8.2 Metrado de Difusores
- Cantidad total de difusores
- CFM total suministrado
- Desglose por ubicación/tamaño

### 8.3 Metrado de Rejillas
- Cantidad total de rejillas
- CFM total de retorno
- Desglose por ubicación/tamaño

### 8.4 Integración con Cotización
Los totales de metrado se pueden copiar directamente a la plantilla de cotización del Cotizador_APU.

---

## 9. Conversiones de Unidades

| De | A | Factor |
|----|---|--------|
| L/s | CFM | × 2.11888 |
| m³/s | CFM | × 2118.88 |
| Pa/m | in.wg/100ft | × 0.12248 |
| m/s | FPM | × 196.85 |
| mm | in | × 0.03937 |
| W | BTU/h | × 3.412 |
| TR | BTU/h | × 12000 |
| TR | W | × 3517 |
| GPM | L/s | × 0.06309 |
| ft | m | × 0.3048 |

---

## 10. Referencias Generales

1. ASHRAE Handbook — Fundamentals (2021)
2. ASHRAE Handbook — HVAC Systems and Equipment (2020)
3. ASHRAE Handbook — Refrigeration (2022)
4. ASHRAE Handbook — Applications (2019)
5. SMACNA — HVAC Duct Construction Standards (2005)
6. ASHRAE Standard 62.1 — Ventilation for Acceptable Indoor Air Quality
7. ASHRAE Standard 55 — Thermal Environmental Conditions for Human Occupancy
8. NEC (NFPA 70) — National Electrical Code
9. NTE E.020 — Instalaciones Eléctricas en Edificios (Perú)
10. Crane Technical Paper 410 — Flow of Fluids Through Valves, Fittings, and Pipe
