# 🥗 NutriPlan — MVP Profesional

> Tu asistente nutricional personal. Planes adapados a ti.

---

## 📋 Resumen del Proyecto

**NutriPlan** es una aplicación móvil de nutrición personalizada que actúa como un asistente nutricional inteligente. Resuelve la dificultad de planificar una alimentación saludable, adaptada a restricciones, objetivos y gustos personales.

---

## 🚀 Cómo ejecutar el prototipo

### Opción 1 — Abrir directamente (más fácil)
```bash
# Simplemente abre el archivo en tu navegador
open index.html
# o en Windows:
start index.html
```

### Opción 2 — Servidor local (recomendado)
```bash
# Con Python (viene preinstalado en Mac/Linux)
python3 -m http.server 3000

# Con Node.js
npx serve .

# Con VS Code: instala "Live Server" y haz click derecho → Open with Live Server
```

Luego abre: `http://localhost:3000`

---

## 📱 Flujo de navegación del prototipo

```
Splash → Login → Onboarding → Dashboard (Home)
                                    ↕
                     Planner ← → Recetas ← → Compras ← → Perfil
```

### Pantallas incluidas:
| Pantalla | Descripción |
|----------|-------------|
| **Splash** | Pantalla de bienvenida con CTA |
| **Login** | Formulario de inicio de sesión |
| **Onboarding** | Configuración de perfil con sliders y opciones |
| **Dashboard** | Resumen diario de calorías, macros y comidas |
| **Planner** | Vista semanal del plan alimentario |
| **Recetas** | Catálogo con filtros y detalle por modal |
| **Lista de compras** | Generada automáticamente del plan semanal |
| **Perfil** | Datos personales, nutricionista y configuración |

---

## 🏗️ Arquitectura del MVP

```
Frontend (React Native / Expo)
    ↓
API REST (Node.js + Express)
    ↓
Base de datos (PostgreSQL)
    ↓
Servicios externos: Auth (Firebase/Supabase), Nutri DB (USDA API)
```

### Stack tecnológico recomendado

| Capa | Tecnología | Justificación |
|------|-----------|----------------|
| Frontend | React Native + Expo | Cross-platform (iOS/Android), rápido para MVP |
| Backend | Node.js + Express | Ecosistema grande, fácil de aprender |
| Base de datos | PostgreSQL + Prisma | Relacional, ideal para datos nutricionales |
| Auth | Supabase Auth | Gratuito, fácil integración |
| Hosting | Railway / Render | Free tier, deploy simple |
| Almacenamiento | Supabase Storage | Para imágenes de recetas |

---

## 🗄️ Estructura de Base de Datos

```sql
-- Usuarios
users (id, email, name, created_at)

-- Perfiles nutricionales
profiles (
  user_id, age, weight_kg, height_cm, sex,
  activity_level, goal, diet_type,
  restrictions[], allergies[], meal_times[]
)

-- Alimentos
foods (id, name, calories, protein, carbs, fat, fiber, category)

-- Recetas
recipes (id, name, description, emoji, calories, protein, carbs, fat,
         prep_time, is_gluten_free, is_vegan, is_vegetarian)

-- Ingredientes de recetas
recipe_ingredients (recipe_id, food_id, quantity, unit)

-- Planes semanales
meal_plans (id, user_id, week_start, created_at)

-- Comidas del plan
plan_meals (
  id, plan_id, day_of_week, meal_type,
  recipe_id, accepted, completed, completed_at
)

-- Registro diario
daily_logs (id, user_id, date, meal_type, recipe_id, calories, notes)

-- Lista de compras
shopping_list (id, user_id, week_start, items[], generated_at)

-- Indicaciones de nutricionista
nutritionist_notes (id, user_id, nutritionist_name, note, created_at, active)
```

---

## 👤 User Persona

**Ana García, 27 años — Santiago, Chile**
- Diseñadora gráfica freelance
- Quiere bajar 8kg en 4 meses
- Intolerante al gluten
- No tiene tiempo para pensar qué comer cada día
- Le frustra MyFitnessPal por ser muy manual
- **Pain point principal:** "Sé que debo comer bien, pero no sé exactamente qué comer"

---

## 🗺️ User Flow

```
1. Descarga app → Ve splash
2. Toca "Comenzar" → Llega al Login/Registro
3. Se registra → Inicia Onboarding (5 pasos)
   - Paso 1: Datos básicos (edad, peso, altura, sexo)
   - Paso 2: Objetivo nutricional
   - Paso 3: Nivel de actividad física
   - Paso 4: Restricciones y alergias
   - Paso 5: Horarios de comida y preferencias
4. App genera plan semanal automático
5. Dashboard: Ve resumen del día
6. Marca comidas como completadas
7. Planner: Acepta/cambia comidas del plan
8. Recetas: Explora y agrega al plan
9. Compras: Ve lista generada automáticamente
10. Perfil: Edita datos, ve indicaciones nutricionista
```

---

## ⚙️ Funcionalidades priorizadas (MoSCoW)

### Must Have (MVP)
- [x] Onboarding con perfil nutricional
- [x] Dashboard diario con macros
- [x] Plan semanal automático
- [x] Registro de comidas (marcar completadas)
- [x] Catálogo de recetas con macros
- [x] Lista de compras automática
- [x] Perfil con restricciones y alergias
- [x] Autenticación básica

### Should Have (v1.1)
- [ ] Notificaciones de horarios de comida
- [ ] Búsqueda avanzada de recetas
- [ ] Registro manual de alimentos
- [ ] Historial semanal/mensual

### Could Have (v2.0)
- [ ] IA para recomendaciones personalizadas
- [ ] Integración con wearables
- [ ] Reconocimiento de imágenes de comida
- [ ] Chat con nutricionista

---

## 💰 Modelo de monetización

### Plan Free
- Plan semanal básico (7 días)
- Hasta 50 recetas
- Dashboard básico
- Lista de compras simple

### Plan Pro — $4.990 CLP/mes
- Plan semanal ilimitado
- +200 recetas premium
- Integración con nutricionista
- Análisis nutricional avanzado
- Sin anuncios

### Plan Nutri (B2B) — $9.990 CLP/mes
- Todo lo anterior
- Portal para nutricionistas
- Seguimiento de múltiples pacientes
- Reportes exportables

---

## 🔮 Roadmap

### Fase 1 — MVP (0-3 meses)
- Prototipo clickable ✅
- Backend básico + auth
- Base de datos de recetas (100+)
- App React Native funcional
- Beta testing con 50 usuarios

### Fase 2 — v1.0 (3-6 meses)
- Lanzamiento App Store + Google Play
- 500 recetas
- Notificaciones push
- Modelo freemium activo

### Fase 3 — v2.0 con IA (6-12 meses)
- Motor de recomendación con ML
- Reconocimiento de imágenes de comida
- Integración con wearables (Apple Watch, Fitbit)
- Portal B2B para nutricionistas
- API pública para partnerships

---

## 🤖 Ideas v2.0 con IA

1. **Recomendador inteligente**: ML que aprende tus gustos y ajusta el plan automáticamente
2. **Foto → nutrición**: Escanea tu plato y obtén macros instantáneos
3. **Chef IA**: Genera recetas únicas basadas en ingredientes que tienes en casa
4. **Predictor de adherencia**: Predice qué días tienes más probabilidad de salirse del plan
5. **Asistente conversacional**: "¿Qué puedo comer si tengo solo 400 kcal restantes?"

---

## 📊 Viabilidad del MVP

**¿Por qué este MVP es viable?**

1. **Técnicamente simple**: No requiere ML complejo, solo CRUD + lógica de planificación
2. **Datos disponibles**: USDA FoodData Central ofrece API gratuita con 300k+ alimentos
3. **Stack probado**: React Native + Node.js tienen enorme comunidad y documentación
4. **Tiempo estimado**: 2-3 desarrolladores pueden construirlo en 3 meses
5. **Costo mínimo**: Free tiers de Supabase, Railway cubren el MVP completo
6. **Mercado validado**: Apps similares tienen millones de usuarios activos en LATAM

---

## 📁 Estructura del proyecto (producción)

```
nutriplan/
├── index.html          ← Prototipo clickable (este archivo)
├── README.md           ← Este documento
│
├── /app (React Native)
│   ├── /screens
│   │   ├── SplashScreen.tsx
│   │   ├── LoginScreen.tsx
│   │   ├── OnboardingScreen.tsx
│   │   ├── HomeScreen.tsx
│   │   ├── PlannerScreen.tsx
│   │   ├── RecipesScreen.tsx
│   │   ├── ShoppingScreen.tsx
│   │   └── ProfileScreen.tsx
│   ├── /components
│   │   ├── MacroCard.tsx
│   │   ├── MealItem.tsx
│   │   ├── RecipeCard.tsx
│   │   └── BottomNav.tsx
│   └── /services
│       ├── api.ts
│       ├── auth.ts
│       └── storage.ts
│
└── /backend (Node.js)
    ├── /routes
    │   ├── auth.js
    │   ├── meals.js
    │   ├── recipes.js
    │   └── plans.js
    ├── /models
    └── server.js
```

---

## 📞 Contacto del proyecto

**NutriPlan** — Proyecto MVP universitario  
Desarrollado como prototipo profesional de startup SaaS de healthtech

---

*Versión del prototipo: 1.0.0 — Mayo 2025*
