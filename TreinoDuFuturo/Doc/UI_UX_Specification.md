# NaNuca - UI/UX Specification for iOS/SwiftUI Implementation

**Version**: 1.0  
**Created**: January 22, 2026  
**Platform**: iOS 17.0+ / SwiftUI  
**Purpose**: Detailed UI/UX specification for AI agent to create native iOS interface

---

## Table of Contents

1. [Design System](#1-design-system)
2. [App Structure & Navigation](#2-app-structure--navigation)
3. [Screen-by-Screen Specifications](#3-screen-by-screen-specifications)
4. [Reusable Components](#4-reusable-components)
5. [Interactions & Animations](#5-interactions--animations)
6. [Accessibility](#6-accessibility)
7. [Implementation Guidelines](#7-implementation-guidelines)

---

## 1. Design System

### 1.1 Color Palette

```swift
// Primary Colors
let accentColor = Color.blue           // Main interactive elements
let backgroundColor = Color(.systemBackground)
let secondaryBackground = Color(.secondarySystemBackground)
let tertiaryBackground = Color(.tertiarySystemBackground)

// Text Colors
let primaryText = Color(.label)
let secondaryText = Color(.secondaryLabel)
let tertiaryText = Color(.tertiaryLabel)

// Status Colors
let successColor = Color.green         // Completed, success states
let warningColor = Color.yellow        // In-progress, attention
let errorColor = Color.red             // Errors, validation failures
let activeColor = Color.orange         // "ATIVO" badge

// Muscle Group Colors (for tags and icons)
let muscleGroupColors: [MuscleGroup: Color] = [
    .chest: .blue,
    .back: .green,
    .legs: .purple,
    .shoulders: .orange,
    .arms: .red,
    .abs: .yellow,
    .cardio: .pink
]

// Exercise Type Colors (for check-in icons)
let exerciseTypeColors: [ExerciseType: Color] = [
    .run: .green,
    .gym: .blue,
    .swim: .cyan,
    .bike: .orange,
    .walk: .mint,
    .yoga: .purple,
    .cycling: .yellow,
    .strengthTraining: .red
]
```

### 1.2 Typography

```swift
// Title Styles
.font(.largeTitle)       // Main screen titles (34pt)
.font(.title)            // Section headers (28pt)
.font(.title2)           // Card titles (22pt)
.font(.title3)           // Sub-section headers (20pt)

// Body Styles
.font(.headline)         // Bold labels, row titles (17pt semibold)
.font(.body)             // Main content (17pt)
.font(.callout)          // Secondary content (16pt)
.font(.subheadline)      // Metadata, timestamps (15pt)

// Caption Styles
.font(.footnote)         // Small labels, hints (13pt)
.font(.caption)          // Very small text, badges (12pt)
.font(.caption2)         // Smallest text (11pt)

// Custom Weights
.fontWeight(.bold)
.fontWeight(.semibold)
.fontWeight(.medium)
.fontWeight(.regular)
```

### 1.3 Spacing System

```swift
// Standard Spacing
let spacing4: CGFloat = 4    // Tight spacing
let spacing8: CGFloat = 8    // Small spacing
let spacing12: CGFloat = 12  // Default spacing
let spacing16: CGFloat = 16  // Section spacing
let spacing20: CGFloat = 20  // Large spacing
let spacing24: CGFloat = 24  // Extra large spacing
let spacing32: CGFloat = 32  // Section breaks

// Content Insets
let listRowInsets = EdgeInsets(top: 12, leading: 16, bottom: 12, trailing: 16)
let cardPadding = EdgeInsets(top: 16, leading: 16, bottom: 16, trailing: 16)
let formPadding: CGFloat = 16
```

### 1.4 Corner Radius

```swift
let radiusSmall: CGFloat = 6   // Small elements, badges
let radiusMedium: CGFloat = 10 // Buttons, tags
let radiusLarge: CGFloat = 12  // Cards, containers
let radiusXL: CGFloat = 16     // Large cards
let radiusCircle: CGFloat = .infinity // Circular elements
```

### 1.5 Shadows

```swift
// Card Shadow
.shadow(color: .black.opacity(0.1), radius: 4, x: 0, y: 2)

// Elevated Shadow
.shadow(color: .black.opacity(0.15), radius: 8, x: 0, y: 4)

// Subtle Shadow
.shadow(color: .black.opacity(0.05), radius: 2, x: 0, y: 1)
```

### 1.6 SF Symbols

```swift
// Navigation Icons
let homeIcon = "house.fill"
let workoutsIcon = "dumbbell.fill"
let progressIcon = "chart.bar.fill"
let checkInIcon = "calendar"

// Action Icons
let addIcon = "plus"
let editIcon = "pencil"
let deleteIcon = "trash"
let saveIcon = "checkmark"
let cancelIcon = "xmark"
let searchIcon = "magnifyingglass"
let filterIcon = "line.3.horizontal.decrease"
let playIcon = "play.fill"
let pauseIcon = "pause.fill"
let skipIcon = "forward.fill"
let cameraIcon = "camera.fill"
let photoIcon = "photo.fill"
let videoIcon = "play.rectangle.fill"

// Status Icons
let completeIcon = "checkmark.circle.fill"
let pendingIcon = "circle"
let inProgressIcon = "circle.lefthalf.filled"
let activeIcon = "star.fill"
let streakIcon = "flame.fill"
let trophyIcon = "trophy.fill"

// Muscle Group Icons
let chestIcon = "figure.strengthtraining.traditional"
let backIcon = "figure.strengthtraining.functional"
let legsIcon = "figure.walk"
let shouldersIcon = "figure.arms.open"
let armsIcon = "figure.boxing"
let absIcon = "figure.core.training"
let cardioIcon = "heart.fill"

// Exercise Type Icons
let runIcon = "figure.run"
let gymIcon = "dumbbell.fill"
let swimIcon = "figure.pool.swim"
let bikeIcon = "bicycle"
let walkIcon = "figure.walk"
let yogaIcon = "figure.yoga"
let cyclingIcon = "figure.outdoor.cycle"
let strengthIcon = "dumbbell.fill"
```

---

## 2. App Structure & Navigation

### 2.1 Root Structure

```
┌─────────────────────────────────────────────────────┐
│                      TabView                         │
├─────────────────────────────────────────────────────┤
│  🏠 Home  │  🏋️ Treinos  │  📊 Progresso  │  📅 Check-in  │
└─────────────────────────────────────────────────────┘
```

```swift
// ContentView.swift
struct ContentView: View {
    var body: some View {
        TabView {
            HomeView()
                .tabItem {
                    Label("Home", systemImage: "house.fill")
                }
            
            WorkoutsTabView()
                .tabItem {
                    Label("Treinos", systemImage: "dumbbell.fill")
                }
            
            ProgressView()
                .tabItem {
                    Label("Progresso", systemImage: "chart.bar.fill")
                }
            
            CheckInView()
                .tabItem {
                    Label("Check-in", systemImage: "calendar")
                }
        }
        .tint(.blue) // Tab accent color
    }
}
```

### 2.2 Navigation Hierarchy

```
Tab 1: Home
├── HomeView
│   ├── → RegisterCheckInView (navigation link)
│   └── → ExecuteWorkoutView (navigation link)

Tab 2: Treinos
├── WorkoutsTabView (Picker: Planos | Biblioteca)
│   ├── Planos → WorkoutPlanListView
│   │   ├── Sheet: CreateWorkoutPlanView
│   │   │   └── Sheet: AddExerciseView
│   │   └── → WorkoutPlanDetailView (navigation link)
│   │       ├── Sheet: EditWorkoutPlanView
│   │       ├── Sheet: SelectExerciseSourceView
│   │       │   ├── Sheet: AddExerciseView
│   │       │   └── Sheet: SelectExistingExerciseView
│   │       └── → ExecuteWorkoutView (navigation link)
│   │           ├── → ExecuteExerciseView (navigation link)
│   │           │   └── Sheet: RestTimerView
│   │           └── → WorkoutSummaryView (navigation link)
│   │
│   └── Biblioteca → ExerciseLibraryView
│       └── Sheet: AddExerciseToLibraryView

Tab 3: Progresso
├── ProgressView (Picker: Treinos | Exercícios)
│   ├── Treinos → WorkoutHistoryListView
│   │   └── → SessionDetailView (navigation link)
│   └── Exercícios → MuscleGroupListView
│       └── → MuscleGroupExercisesView (navigation link)
│           └── → ExerciseHistoryView (navigation link)

Tab 4: Check-in
├── CheckInView
│   ├── → RegisterCheckInView (navigation link)
│   └── → ViewAllCheckInsView (navigation link)
```

---

## 3. Screen-by-Screen Specifications

### 3.1 Home Tab - HomeView

**Purpose**: Dashboard with key information and quick actions

**Layout Structure**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
├─────────────────────────────────────┤
│ ScrollView                          │
│ ┌─────────────────────────────────┐ │
│ │ GREETING SECTION                │ │
│ │ "Olá, Atleta!"                  │ │
│ │ "22 de Janeiro, 2026"           │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ CHECK-IN CARD                   │ │
│ │ ┌───────────────────────────┐  │ │
│ │ │ 📅 Check-in Diário        │  │ │
│ │ │                           │  │ │
│ │ │ [If not done today:]      │  │ │
│ │ │ "Registre seu treino"     │  │ │
│ │ │ [Fazer Check-in →]        │  │ │
│ │ │                           │  │ │
│ │ │ [If done today:]          │  │ │
│ │ │ ✓ "Check-in realizado!"   │  │ │
│ │ │ "Há 2 horas"              │  │ │
│ │ └───────────────────────────┘  │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ ACTIVE PLAN CARD                │ │
│ │ ┌───────────────────────────┐  │ │
│ │ │ 🏋️ Plano Ativo            │  │ │
│ │ │                           │  │ │
│ │ │ [If has active plan:]     │  │ │
│ │ │ "Treino de Peito"         │  │ │
│ │ │ "5 exercícios"            │  │ │
│ │ │ [Iniciar Treino →]        │  │ │
│ │ │                           │  │ │
│ │ │ [If no active plan:]      │  │ │
│ │ │ "Nenhum plano ativo"      │  │ │
│ │ │ "Ative um plano na aba    │  │ │
│ │ │  Treinos"                 │  │ │
│ │ └───────────────────────────┘  │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ LAST WORKOUT CARD               │ │
│ │ ┌───────────────────────────┐  │ │
│ │ │ ⏱️ Último Treino          │  │ │
│ │ │                           │  │ │
│ │ │ [If has workout:]         │  │ │
│ │ │ "Treino de Peito"         │  │ │
│ │ │ "Há 2 dias • 45 min"      │  │ │
│ │ │                           │  │ │
│ │ │ [If no workouts:]         │  │ │
│ │ │ (Card hidden)             │  │ │
│ │ └───────────────────────────┘  │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

**SwiftUI Implementation**:
```swift
struct HomeView: View {
    @Environment(\.modelContext) private var modelContext
    @State private var viewModel = HomeViewModel()
    
    var body: some View {
        NavigationStack {
            ScrollView {
                VStack(spacing: 20) {
                    // Greeting Section
                    greetingSection
                    
                    // Check-in Card
                    checkInCard
                    
                    // Active Plan Card
                    activePlanCard
                    
                    // Last Workout Card (conditional)
                    if viewModel.lastSession != nil {
                        lastWorkoutCard
                    }
                }
                .padding()
            }
            .navigationTitle("Home")
            .onAppear {
                viewModel.loadData(context: modelContext)
            }
        }
    }
}
```

**Card Design Specifications**:
- Background: `.secondarySystemBackground`
- Corner radius: 16pt
- Padding: 16pt all sides
- Shadow: subtle (0.1 opacity, 4pt radius)
- Icon: left-aligned, 24pt, colored
- Title: `.headline`, primary color
- Subtitle: `.subheadline`, secondary color
- Button: blue text, chevron.right

---

### 3.2 Treinos Tab - WorkoutsTabView

**Purpose**: Container for Plans and Library segments

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
├─────────────────────────────────────┤
│ ┌─────────────────────────────────┐ │
│ │    [Planos]  |  [Biblioteca]    │ │
│ │    Picker(segmented)            │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │  Content based on selection     │ │
│ │                                 │ │
│ │  • WorkoutPlanListView          │ │
│ │  • ExerciseLibraryView          │ │
│ │                                 │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

```swift
struct WorkoutsTabView: View {
    @State private var selectedTab: WorkoutsTab = .plans
    
    enum WorkoutsTab: String, CaseIterable {
        case plans = "Planos"
        case library = "Biblioteca"
    }
    
    var body: some View {
        NavigationStack {
            VStack(spacing: 0) {
                // Segmented Picker
                Picker("", selection: $selectedTab) {
                    ForEach(WorkoutsTab.allCases, id: \.self) { tab in
                        Text(tab.rawValue).tag(tab)
                    }
                }
                .pickerStyle(.segmented)
                .padding(.horizontal)
                .padding(.top, 8)
                
                // Content
                switch selectedTab {
                case .plans:
                    WorkoutPlanListView()
                case .library:
                    ExerciseLibraryView()
                }
            }
            .navigationTitle("Treinos")
        }
    }
}
```

---

### 3.3 WorkoutPlanListView

**Purpose**: List all workout plans with search and create functionality

**Layout**:
```
┌─────────────────────────────────────┐
│ 🔍 Buscar planos...                 │  ← SearchBar
├─────────────────────────────────────┤
│                                     │
│ [EMPTY STATE - if no plans]         │
│ ┌─────────────────────────────────┐ │
│ │       🏋️                        │ │
│ │  "Nenhum plano criado"          │ │
│ │  "Crie seu primeiro plano"      │ │
│ │  [Criar Plano]                  │ │
│ └─────────────────────────────────┘ │
│                                     │
│ [LIST - if has plans]               │
│ ┌─────────────────────────────────┐ │
│ │ Treino de Peito        ATIVO   │ │  ← Row with badge
│ │ 5 exercícios • Há 2 dias        │ │
│ ├─────────────────────────────────┤ │
│ │ Treino de Pernas               │ │
│ │ 6 exercícios • Há 1 semana      │ │
│ ├─────────────────────────────────┤ │
│ │ Treino de Costas               │ │
│ │ 4 exercícios • Há 2 semanas     │ │
│ └─────────────────────────────────┘ │
│                                     │
│ [SEARCH EMPTY STATE]                │
│ ContentUnavailableView.search       │
│                                     │
└─────────────────────────────────────┘
         Toolbar: [ + ]  ← Add button
```

**Row Design (WorkoutPlanRowView)**:
```
┌─────────────────────────────────────┐
│ Plan Name                    ATIVO  │  ← .headline + orange badge
│ X exercícios • Há Y dias            │  ← .subheadline, secondary
│                              >      │  ← chevron.right
└─────────────────────────────────────┘
```

```swift
struct WorkoutPlanRowView: View {
    let plan: WorkoutPlan
    
    var body: some View {
        HStack {
            VStack(alignment: .leading, spacing: 4) {
                HStack {
                    Text(plan.name)
                        .font(.headline)
                    
                    if plan.isActive {
                        Text("ATIVO")
                            .font(.caption2)
                            .fontWeight(.bold)
                            .foregroundStyle(.white)
                            .padding(.horizontal, 6)
                            .padding(.vertical, 2)
                            .background(Color.orange)
                            .clipShape(Capsule())
                    }
                }
                
                Text("\(plan.exercises.count) exercícios • \(plan.modifiedDate.relativeTime)")
                    .font(.subheadline)
                    .foregroundStyle(.secondary)
            }
            
            Spacer()
            
            Image(systemName: "chevron.right")
                .font(.caption)
                .foregroundStyle(.tertiary)
        }
        .contentShape(Rectangle())
    }
}
```

**Swipe Actions**:
- Swipe left: Delete button (red, destructive)
- Confirmation alert before delete

---

### 3.4 CreateWorkoutPlanView (Sheet)

**Purpose**: Form to create a new workout plan

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
│ Title: "Novo Plano"                 │
│ Toolbar: [Cancelar]  ...  [Salvar]  │
├─────────────────────────────────────┤
│ Form                                │
│ ┌─────────────────────────────────┐ │
│ │ Section: "Informações"          │ │
│ │                                 │ │
│ │ Nome do Plano *                 │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ TextField                   │ │ │
│ │ └─────────────────────────────┘ │ │
│ │ [Validation error if empty]     │ │
│ │                                 │ │
│ │ Descrição                       │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ TextEditor (3 lines)        │ │ │
│ │ └─────────────────────────────┘ │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ Section: "Exercícios"           │ │
│ │                                 │ │
│ │ [List of added exercises]       │ │
│ │ ┌───────────────────────────┐   │ │
│ │ │ 🔵 Supino Reto    Peito   │   │ │
│ │ │ 4 × 10 • 90s              │   │ │
│ │ └───────────────────────────┘   │ │
│ │                                 │ │
│ │ [+ Adicionar Exercício]         │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

**Validation**:
- Name field: red border when empty and touched
- Save button disabled until name is valid
- Show inline error message below field

---

### 3.5 AddExerciseView (Sheet)

**Purpose**: Form to add an exercise to a plan or library

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
│ Title: "Novo Exercício"             │
│ Toolbar: [Cancelar]  ...  [Salvar]  │
├─────────────────────────────────────┤
│ Form                                │
│ ┌─────────────────────────────────┐ │
│ │ Section: "Informações"          │ │
│ │                                 │ │
│ │ Nome do Exercício *             │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ TextField                   │ │ │
│ │ └─────────────────────────────┘ │ │
│ │                                 │ │
│ │ Grupo Muscular                  │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ Picker (menu style)         │ │ │
│ │ │ [Peito ▼]                   │ │ │
│ │ └─────────────────────────────┘ │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ Section: "Configuração"         │ │
│ │                                 │ │
│ │ Séries                    [3]   │ │  ← Stepper (1-99)
│ │ Repetições               [12]   │ │  ← Stepper (1-99)
│ │ Descanso (seg)           [60]   │ │  ← Stepper (0-999)
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ Section: "Opcional"             │ │
│ │                                 │ │
│ │ URL do Vídeo                    │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ TextField (URL keyboard)    │ │ │
│ │ └─────────────────────────────┘ │ │
│ │                                 │ │
│ │ [Toggle] Salvar na Biblioteca   │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

**Muscle Group Picker Options**:
- Peito (chest icon, blue)
- Costas (back icon, green)
- Pernas (legs icon, purple)
- Ombros (shoulders icon, orange)
- Braços (arms icon, red)
- Abdômen (abs icon, yellow)
- Cardio (cardio icon, pink)

---

### 3.6 WorkoutPlanDetailView

**Purpose**: View plan details and start workout

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
│ Title: "Treino de Peito"            │
│ Toolbar: [...] Menu                 │
├─────────────────────────────────────┤
│ ScrollView                          │
│ ┌─────────────────────────────────┐ │
│ │ HEADER INFO                     │ │
│ │                                 │ │
│ │ "Foco em peito e tríceps"       │ │  ← Description
│ │ Criado: 15/01/2026              │ │
│ │                                 │ │
│ │ [ATIVO badge if active]         │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ Section: "Exercícios" (5)       │ │
│ │                                 │ │
│ │ ┌───────────────────────────┐   │ │
│ │ │ 🔵 Supino Reto    [Peito] │   │ │
│ │ │    4 × 10 • 90s descanso  │   │ │
│ │ │                      🎬   │   │ │  ← Video icon if URL
│ │ ├───────────────────────────┤   │ │
│ │ │ 🔵 Supino Inclinado[Peito]│   │ │
│ │ │    4 × 10 • 90s descanso  │   │ │
│ │ ├───────────────────────────┤   │ │
│ │ │ 🔴 Tríceps Corda  [Braços]│   │ │
│ │ │    3 × 12 • 60s descanso  │   │ │
│ │ └───────────────────────────┘   │ │
│ │                                 │ │
│ │ [+ Adicionar Exercício]         │ │
│ └─────────────────────────────────┘ │
│                                     │
│ [EMPTY STATE if no exercises]       │
│ "Nenhum exercício adicionado"       │
│                                     │
└─────────────────────────────────────┘
│ ┌─────────────────────────────────┐ │
│ │  [     Iniciar Treino     ]    │ │  ← Primary Button
│ └─────────────────────────────────┘ │
```

**Toolbar Menu Options**:
```swift
Menu {
    Button("Editar", systemImage: "pencil") { }
    Button(plan.isActive ? "Desativar" : "Ativar", 
           systemImage: plan.isActive ? "star.slash" : "star.fill") { }
    Divider()
    Button("Apagar", systemImage: "trash", role: .destructive) { }
} label: {
    Image(systemName: "ellipsis.circle")
}
```

---

### 3.7 ExecuteWorkoutView

**Purpose**: Active workout session with exercise list and progress

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
│ Title: "Treino de Peito"            │
├─────────────────────────────────────┤
│ ┌─────────────────────────────────┐ │
│ │ PROGRESS HEADER                 │ │
│ │                                 │ │
│ │ 3/5 exercícios completos        │ │
│ │ ████████████░░░░░░  60%         │ │  ← Progress bar
│ │                                 │ │
│ │ Duração: 25:32                  │ │
│ └─────────────────────────────────┘ │
│                                     │
│ List                                │
│ ┌─────────────────────────────────┐ │
│ │ ✅ Supino Reto                  │ │  ← Green checkmark
│ │    4/4 séries completas         │ │
│ ├─────────────────────────────────┤ │
│ │ ✅ Supino Inclinado             │ │
│ │    4/4 séries completas         │ │
│ ├─────────────────────────────────┤ │
│ │ 🟡 Crossover                    │ │  ← Yellow in-progress
│ │    2/4 séries • Em andamento    │ │
│ ├─────────────────────────────────┤ │
│ │ ⚪ Tríceps Corda                │ │  ← Gray pending
│ │    0/3 séries • Pendente        │ │
│ ├─────────────────────────────────┤ │
│ │ ⚪ Tríceps Francês              │ │
│ │    0/3 séries • Pendente        │ │
│ └─────────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
│ ┌─────────────────────────────────┐ │
│ │  [    Finalizar Treino    ]    │ │  ← Secondary Button
│ └─────────────────────────────────┘ │
```

**Exercise Status Badges**:
- ✅ Complete (green): `checkmark.circle.fill`
- 🟡 In Progress (yellow): `circle.lefthalf.filled`
- ⚪ Pending (gray): `circle`

**Row Tap**: Navigate to ExecuteExerciseView

---

### 3.8 ExecuteExerciseView

**Purpose**: Log sets for a specific exercise during workout

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
│ Title: "Supino Reto"                │
│ Subtitle: "Peito"                   │
├─────────────────────────────────────┤
│ ScrollView                          │
│ ┌─────────────────────────────────┐ │
│ │ LAST WORKOUT REFERENCE          │ │
│ │                                 │ │
│ │ "Último treino:"                │ │
│ │ "80kg × 10 reps"                │ │  ← Bold, accent color
│ │ "Há 5 dias"                     │ │
│ │                                 │ │
│ │ [Hidden if first time]          │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ COMPLETED SETS                  │ │
│ │                                 │ │
│ │ ┌───────────────────────────┐   │ │
│ │ │  1  │ 80kg × 10          │   │ │  ← Completed set row
│ │ ├───────────────────────────┤   │ │
│ │ │  2  │ 80kg × 8           │   │ │
│ │ └───────────────────────────┘   │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ CURRENT SET INPUT               │ │
│ │ "Série 3 de 4"                  │ │
│ │                                 │ │
│ │ Peso (kg)          Repetições   │ │
│ │ ┌──────────────┐  ┌──────────┐ │ │
│ │ │     80       │  │    10    │ │ │
│ │ └──────────────┘  └──────────┘ │ │
│ │ [Validation error messages]     │ │
│ │                                 │ │
│ │ [     Salvar Série     ]        │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ [    Marcar como Completo    ] │ │  ← Secondary, outline
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

**Input Validation**:
- Weight: optional (empty = bodyweight), must be positive number if filled
- Reps: required, must be positive integer
- Real-time validation with red border and error message
- Save button disabled until valid

**After Save**: Automatically show RestTimerView (except on last set)

---

### 3.9 RestTimerView (Sheet)

**Purpose**: Rest countdown timer between sets

**Layout**:
```
┌─────────────────────────────────────┐
│ Sheet (presentationDetents: [.medium])│
├─────────────────────────────────────┤
│              Center                 │
│                                     │
│    ┌─────────────────────────┐      │
│    │                         │      │
│    │    ⭕ Circular Progress │      │
│    │         (animated)      │      │
│    │                         │      │
│    │         45              │      │  ← Large countdown
│    │       segundos          │      │
│    │                         │      │
│    └─────────────────────────┘      │
│                                     │
│        "Próxima série: 4 de 4"      │
│                                     │
│    ┌─────────┐    ┌─────────┐      │
│    │  ⏸️     │    │   ⏭️    │      │
│    │ Pausar  │    │  Pular  │      │
│    └─────────┘    └─────────┘      │
│                                     │
└─────────────────────────────────────┘

[When paused:]
│    │  ▶️     │    │   ⏭️    │      │
│    │ Retomar │    │  Pular  │      │
```

**Circular Progress Specifications**:
- Size: 200pt diameter
- Stroke width: 12pt
- Background: gray (0.2 opacity)
- Progress: accent color (blue)
- Animation: smooth countdown
- Stroke cap: rounded

**Timer Completion**:
1. Haptic feedback: `.medium` impact
2. Audio: system sound (respects silent mode)
3. Auto-dismiss after 1 second

---

### 3.10 WorkoutSummaryView

**Purpose**: Summary after completing a workout

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
│ Title: "Treino Finalizado!"         │
├─────────────────────────────────────┤
│              Center                 │
│                                     │
│         🎉                          │  ← Large celebration icon
│                                     │
│    "Parabéns!"                      │
│    "Você completou seu treino"      │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ STATS GRID                      │ │
│ │                                 │ │
│ │  ┌─────────┐  ┌─────────┐       │ │
│ │  │ ⏱️      │  │ 🏋️      │       │ │
│ │  │ 45:32   │  │   5     │       │ │
│ │  │ Duração │  │Exercícios│       │ │
│ │  └─────────┘  └─────────┘       │ │
│ │                                 │ │
│ │  ┌─────────┐  ┌─────────┐       │ │
│ │  │ 📊      │  │ 🔢      │       │ │
│ │  │   18    │  │  156    │       │ │
│ │  │ Séries  │  │  Reps   │       │ │
│ │  └─────────┘  └─────────┘       │ │
│ └─────────────────────────────────┘ │
│                                     │
│    "Treino de Peito"                │  ← Plan name
│    "22/01/2026 às 15:30"            │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │  [       Concluir        ]     │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │  [    Fazer Check-in     ]     │ │  ← Optional, secondary
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

---

### 3.11 Check-in Tab - CheckInView

**Purpose**: Calendar view of check-ins with statistics

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
│ Title: "Check-in"                   │
├─────────────────────────────────────┤
│ ScrollView                          │
│ ┌─────────────────────────────────┐ │
│ │ STATS SECTION                   │ │
│ │                                 │ │
│ │ ┌───────────────────────────┐   │ │
│ │ │  🏆 Total Check-ins: 47   │   │ │
│ │ └───────────────────────────┘   │ │
│ │                                 │ │
│ │ ┌───────────┐  ┌───────────┐    │ │
│ │ │ 🔥 5      │  │ ⭐ 14     │    │ │
│ │ │ Sequência │  │ Melhor    │    │ │
│ │ │  Atual    │  │ Sequência │    │ │
│ │ └───────────┘  └───────────┘    │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ CALENDAR - Janeiro 2026         │ │
│ │                                 │ │
│ │  D   S   T   Q   Q   S   S      │ │
│ │ ┌───┬───┬───┬───┬───┬───┬───┐  │ │
│ │ │   │   │   │ 1 │ 2 │ 3 │ 4 │  │ │
│ │ ├───┼───┼───┼───┼───┼───┼───┤  │ │
│ │ │ 5 │ 6 │ 7 │ 8 │ 9 │10 │11 │  │ │
│ │ │🏃│🏋️│   │🏊│   │🚴│🧘│  │ │  ← Icons or photos
│ │ ├───┼───┼───┼───┼───┼───┼───┤  │ │
│ │ │12 │13 │14 │15 │16 │17 │18 │  │ │
│ │ │📷│📷│   │📷│📷│📷│   │  │ │  ← Photos if available
│ │ └───┴───┴───┴───┴───┴───┴───┘  │ │
│ └─────────────────────────────────┘ │
│                                     │
│ [Ver Todos os Check-ins →]          │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │  [     Fazer Check-in     ]    │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

**Calendar Day Cell (CheckInDayCell)**:
```swift
struct CheckInDayCell: View {
    let date: Date
    let checkIn: CheckIn?
    
    var body: some View {
        VStack(spacing: 2) {
            Text("\(date.day)")
                .font(.caption)
            
            if let checkIn = checkIn {
                if let photoData = checkIn.photoData,
                   let image = UIImage(data: photoData) {
                    // Photo thumbnail
                    Image(uiImage: image)
                        .resizable()
                        .aspectRatio(contentMode: .fill)
                        .frame(width: 32, height: 32)
                        .clipShape(Circle())
                } else {
                    // Exercise type icon
                    Image(systemName: checkIn.exerciseType.iconName)
                        .font(.caption)
                        .foregroundStyle(checkIn.exerciseType.color)
                        .frame(width: 32, height: 32)
                        .background(checkIn.exerciseType.color.opacity(0.2))
                        .clipShape(Circle())
                }
            } else {
                // Empty cell
                Circle()
                    .fill(Color.clear)
                    .frame(width: 32, height: 32)
            }
        }
        .frame(maxWidth: .infinity)
    }
}
```

---

### 3.12 RegisterCheckInView

**Purpose**: Form to register a new check-in

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
│ Title: "Novo Check-in"              │
│ Toolbar: [Cancelar]  ...  [Check In]│
├─────────────────────────────────────┤
│ Form                                │
│ ┌─────────────────────────────────┐ │
│ │ PHOTO SECTION                   │ │
│ │                                 │ │
│ │ [If no photo:]                  │ │
│ │ ┌───────────────────────────┐   │ │
│ │ │         📷               │   │ │
│ │ │    Adicionar Foto        │   │ │  ← Dashed border
│ │ │                          │   │ │
│ │ └───────────────────────────┘   │ │
│ │                                 │ │
│ │ [If has photo:]                 │ │
│ │ ┌───────────────────────────┐   │ │
│ │ │      [Photo Preview]      │   │ │  ← Large preview
│ │ │                          │   │ │
│ │ │  [Trocar]    [Remover]   │   │ │
│ │ └───────────────────────────┘   │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ Section: "Detalhes"             │ │
│ │                                 │ │
│ │ Tipo de Exercício *             │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ Picker (menu style)         │ │ │
│ │ │ [🏋️ Gym ▼]                  │ │ │
│ │ └─────────────────────────────┘ │ │
│ │                                 │ │
│ │ Título *                        │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ "Treino pesado hoje!"       │ │ │
│ │ └─────────────────────────────┘ │ │
│ │                                 │ │
│ │ Data e Hora                     │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ DatePicker (compact)        │ │ │
│ │ └─────────────────────────────┘ │ │
│ └─────────────────────────────────┘ │
│                                     │
│ ┌─────────────────────────────────┐ │
│ │ Section: "Opcional"             │ │
│ │                                 │ │
│ │ Calorias                        │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ TextField (number pad)      │ │ │
│ │ └─────────────────────────────┘ │ │
│ │                                 │ │
│ │ Local                           │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ "Smart Fit Academia"        │ │ │
│ │ └─────────────────────────────┘ │ │
│ │                                 │ │
│ │ Observações                     │ │
│ │ ┌─────────────────────────────┐ │ │
│ │ │ TextEditor (3 lines)        │ │ │
│ │ └─────────────────────────────┘ │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

**Photo Selection Action Sheet**:
```swift
.confirmationDialog("Adicionar Foto", isPresented: $showPhotoOptions) {
    Button("Tirar Foto") { showCamera = true }
    Button("Escolher da Galeria") { showPhotoPicker = true }
    Button("Cancelar", role: .cancel) { }
}
```

**Exercise Type Picker Options**:
- 🏃 Corrida (Run)
- 🏋️ Academia (Gym)
- 🏊 Natação (Swim)
- 🚴 Bicicleta (Bike)
- 🚶 Caminhada (Walk)
- 🧘 Yoga
- 🚲 Ciclismo (Cycling)
- 💪 Musculação (Strength Training)

---

### 3.13 Progress Tab - ProgressView

**Purpose**: View workout history and exercise statistics

**Layout**:
```
┌─────────────────────────────────────┐
│ NavigationStack                      │
│ Title: "Progresso"                  │
├─────────────────────────────────────┤
│ ┌─────────────────────────────────┐ │
│ │   [Treinos]  |  [Exercícios]   │ │  ← Segmented Picker
│ └─────────────────────────────────┘ │
│                                     │
│ [TREINOS TAB:]                      │
│ WorkoutHistoryListView              │
│ ┌─────────────────────────────────┐ │
│ │ ┌───────────────────────────┐   │ │
│ │ │ 22/01/2026 • 15:30        │   │ │
│ │ │ Treino de Peito           │   │ │
│ │ │ 45 min • ✅ Completo      │   │ │
│ │ ├───────────────────────────┤   │ │
│ │ │ 20/01/2026 • 16:00        │   │ │
│ │ │ Treino de Pernas          │   │ │
│ │ │ 52 min • ✅ Completo      │   │ │
│ │ └───────────────────────────┘   │ │
│ └─────────────────────────────────┘ │
│                                     │
│ [EXERCÍCIOS TAB:]                   │
│ MuscleGroupListView                 │
│ ┌─────────────────────────────────┐ │
│ │ LazyVGrid (2 columns)           │ │
│ │                                 │ │
│ │ ┌──────────┐  ┌──────────┐      │ │
│ │ │  🔵 Peito │  │  🟢 Costas│      │ │
│ │ │  12 exer. │  │  8 exer. │      │ │
│ │ └──────────┘  └──────────┘      │ │
│ │                                 │ │
│ │ ┌──────────┐  ┌──────────┐      │ │
│ │ │  🟣 Pernas│  │  🟠 Ombros│      │ │
│ │ │  15 exer. │  │  6 exer. │      │ │
│ │ └──────────┘  └──────────┘      │ │
│ │                                 │ │
│ │ ┌──────────┐  ┌──────────┐      │ │
│ │ │  🔴 Braços│  │  🟡 Abdôm.│      │ │
│ │ │  10 exer. │  │  4 exer. │      │ │
│ │ └──────────┘  └──────────┘      │ │
│ │                                 │ │
│ │ ┌──────────┐                    │ │
│ │ │  🩷 Cardio│                    │ │
│ │ │  3 exer. │                    │ │
│ │ └──────────┘                    │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

**Muscle Group Card Design**:
```swift
struct MuscleGroupCard: View {
    let muscleGroup: MuscleGroup
    let exerciseCount: Int
    
    var body: some View {
        VStack(spacing: 8) {
            Image(systemName: muscleGroup.iconName)
                .font(.largeTitle)
                .foregroundStyle(muscleGroup.tagColor)
            
            Text(muscleGroup.displayName)
                .font(.headline)
            
            Text("\(exerciseCount) exercícios")
                .font(.caption)
                .foregroundStyle(.secondary)
        }
        .frame(maxWidth: .infinity)
        .padding()
        .background(Color(.secondarySystemBackground))
        .clipShape(RoundedRectangle(cornerRadius: 12))
    }
}
```

---

### 3.14 ExerciseLibraryView

**Purpose**: Global exercise library grouped by muscle group

**Layout**:
```
┌─────────────────────────────────────┐
│ 🔍 Buscar exercícios...             │  ← SearchBar
├─────────────────────────────────────┤
│ [Filter: Todos ▼]                   │  ← Muscle group filter
│                                     │
│ [EMPTY STATE if no exercises]       │
│ "Sua biblioteca está vazia"         │
│ "Adicione exercícios para           │
│  reutilizar em seus planos"         │
│ [+ Adicionar Exercício]             │
│                                     │
│ [LIST grouped by muscle]            │
│ Section: "Peito" (4)                │
│ ┌─────────────────────────────────┐ │
│ │ Supino Reto                     │ │
│ │ 4 × 10 • 90s                    │ │
│ ├─────────────────────────────────┤ │
│ │ Supino Inclinado                │ │
│ │ 4 × 10 • 90s                    │ │
│ └─────────────────────────────────┘ │
│                                     │
│ Section: "Costas" (3)               │
│ ┌─────────────────────────────────┐ │
│ │ Puxada Frontal                  │ │
│ │ 4 × 12 • 60s                    │ │
│ └─────────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
         Toolbar: [ + ]  ← Add button
```

---

## 4. Reusable Components

### 4.1 PrimaryButton

```swift
struct PrimaryButton: View {
    let title: String
    var systemImage: String? = nil
    var isEnabled: Bool = true
    var isLoading: Bool = false
    let action: () -> Void
    
    var body: some View {
        Button(action: action) {
            HStack(spacing: 8) {
                if isLoading {
                    ProgressView()
                        .tint(.white)
                } else {
                    if let systemImage {
                        Image(systemName: systemImage)
                    }
                    Text(title)
                        .fontWeight(.semibold)
                }
            }
            .frame(maxWidth: .infinity)
            .padding(.vertical, 14)
            .background(isEnabled ? Color.blue : Color.gray)
            .foregroundStyle(.white)
            .clipShape(RoundedRectangle(cornerRadius: 12))
        }
        .disabled(!isEnabled || isLoading)
        .opacity(isEnabled ? 1.0 : 0.6)
    }
}
```

### 4.2 SecondaryButton

```swift
struct SecondaryButton: View {
    let title: String
    var systemImage: String? = nil
    let action: () -> Void
    
    var body: some View {
        Button(action: action) {
            HStack(spacing: 8) {
                if let systemImage {
                    Image(systemName: systemImage)
                }
                Text(title)
                    .fontWeight(.medium)
            }
            .frame(maxWidth: .infinity)
            .padding(.vertical, 14)
            .background(Color(.secondarySystemBackground))
            .foregroundStyle(.blue)
            .clipShape(RoundedRectangle(cornerRadius: 12))
            .overlay(
                RoundedRectangle(cornerRadius: 12)
                    .stroke(Color.blue, lineWidth: 1)
            )
        }
    }
}
```

### 4.3 EmptyStateView

```swift
struct EmptyStateView: View {
    let icon: String
    let title: String
    let message: String
    var buttonTitle: String? = nil
    var buttonAction: (() -> Void)? = nil
    
    var body: some View {
        VStack(spacing: 16) {
            Image(systemName: icon)
                .font(.system(size: 60))
                .foregroundStyle(.secondary)
            
            Text(title)
                .font(.title2)
                .fontWeight(.semibold)
            
            Text(message)
                .font(.body)
                .foregroundStyle(.secondary)
                .multilineTextAlignment(.center)
                .padding(.horizontal, 32)
            
            if let buttonTitle, let buttonAction {
                PrimaryButton(title: buttonTitle, action: buttonAction)
                    .frame(width: 200)
                    .padding(.top, 8)
            }
        }
        .frame(maxWidth: .infinity, maxHeight: .infinity)
    }
}
```

### 4.4 ValidationTextField

```swift
struct ValidationTextField: View {
    let title: String
    @Binding var text: String
    var placeholder: String = ""
    var isRequired: Bool = false
    var errorMessage: String? = nil
    var keyboardType: UIKeyboardType = .default
    
    private var isError: Bool {
        errorMessage != nil && !text.isEmpty
    }
    
    var body: some View {
        VStack(alignment: .leading, spacing: 4) {
            HStack {
                Text(title)
                    .font(.subheadline)
                if isRequired {
                    Text("*")
                        .foregroundStyle(.red)
                }
            }
            
            TextField(placeholder, text: $text)
                .keyboardType(keyboardType)
                .padding(12)
                .background(Color(.tertiarySystemBackground))
                .clipShape(RoundedRectangle(cornerRadius: 8))
                .overlay(
                    RoundedRectangle(cornerRadius: 8)
                        .stroke(isError ? Color.red : Color.clear, lineWidth: 1)
                )
            
            if let errorMessage, isError {
                HStack(spacing: 4) {
                    Image(systemName: "exclamationmark.circle.fill")
                    Text(errorMessage)
                }
                .font(.caption)
                .foregroundStyle(.red)
            }
        }
    }
}
```

### 4.5 MuscleGroupTag

```swift
struct MuscleGroupTag: View {
    let muscleGroup: MuscleGroup
    var size: TagSize = .medium
    
    enum TagSize {
        case small, medium, large
        
        var font: Font {
            switch self {
            case .small: return .caption2
            case .medium: return .caption
            case .large: return .footnote
            }
        }
        
        var padding: EdgeInsets {
            switch self {
            case .small: return EdgeInsets(top: 2, leading: 6, bottom: 2, trailing: 6)
            case .medium: return EdgeInsets(top: 4, leading: 8, bottom: 4, trailing: 8)
            case .large: return EdgeInsets(top: 6, leading: 10, bottom: 6, trailing: 10)
            }
        }
    }
    
    var body: some View {
        Text(muscleGroup.displayName)
            .font(size.font)
            .fontWeight(.medium)
            .foregroundStyle(muscleGroup.tagColor)
            .padding(size.padding)
            .background(muscleGroup.tagColor.opacity(0.15))
            .clipShape(Capsule())
    }
}
```

### 4.6 CircularProgressView

```swift
struct CircularProgressView: View {
    let progress: Double // 0.0 to 1.0
    var lineWidth: CGFloat = 12
    var strokeColor: Color = .blue
    var backgroundColor: Color = .gray.opacity(0.2)
    
    var body: some View {
        ZStack {
            // Background circle
            Circle()
                .stroke(backgroundColor, lineWidth: lineWidth)
            
            // Progress arc
            Circle()
                .trim(from: 0, to: progress)
                .stroke(
                    strokeColor,
                    style: StrokeStyle(
                        lineWidth: lineWidth,
                        lineCap: .round
                    )
                )
                .rotationEffect(.degrees(-90))
                .animation(.linear(duration: 1), value: progress)
        }
    }
}
```

### 4.7 StatCard

```swift
struct StatCard: View {
    let icon: String
    let value: String
    let label: String
    var iconColor: Color = .blue
    
    var body: some View {
        VStack(spacing: 8) {
            Image(systemName: icon)
                .font(.title2)
                .foregroundStyle(iconColor)
            
            Text(value)
                .font(.title)
                .fontWeight(.bold)
            
            Text(label)
                .font(.caption)
                .foregroundStyle(.secondary)
        }
        .frame(maxWidth: .infinity)
        .padding()
        .background(Color(.secondarySystemBackground))
        .clipShape(RoundedRectangle(cornerRadius: 12))
    }
}
```

---

## 5. Interactions & Animations

### 5.1 Navigation Transitions

```swift
// Standard push navigation
NavigationLink(destination: DestinationView()) {
    RowView()
}

// Sheet presentation
.sheet(isPresented: $isShowingSheet) {
    SheetView()
}

// Full screen cover (for camera)
.fullScreenCover(isPresented: $isShowingCamera) {
    CameraView()
}
```

### 5.2 List Interactions

```swift
// Swipe to delete
.swipeActions(edge: .trailing, allowsFullSwipe: true) {
    Button(role: .destructive) {
        deleteAction()
    } label: {
        Label("Apagar", systemImage: "trash")
    }
}

// Pull to refresh (if needed)
.refreshable {
    await refreshData()
}
```

### 5.3 Button Feedback

```swift
// Haptic feedback on tap
Button(action: {
    let generator = UIImpactFeedbackGenerator(style: .light)
    generator.impactOccurred()
    action()
}) {
    // Button content
}
```

### 5.4 Progress Animations

```swift
// Animated progress bar
struct AnimatedProgressBar: View {
    let progress: Double
    
    var body: some View {
        GeometryReader { geometry in
            ZStack(alignment: .leading) {
                // Background
                RoundedRectangle(cornerRadius: 4)
                    .fill(Color.gray.opacity(0.2))
                
                // Progress
                RoundedRectangle(cornerRadius: 4)
                    .fill(progress > 0.8 ? Color.green : Color.blue)
                    .frame(width: geometry.size.width * progress)
                    .animation(.easeInOut(duration: 0.3), value: progress)
            }
        }
        .frame(height: 8)
    }
}
```

### 5.5 Timer Animation

```swift
// Rest timer countdown animation
struct RestTimerView: View {
    @State private var progress: Double = 1.0
    let duration: Int
    
    var body: some View {
        CircularProgressView(progress: progress)
            .onAppear {
                withAnimation(.linear(duration: Double(duration))) {
                    progress = 0.0
                }
            }
    }
}
```

---

## 6. Accessibility

### 6.1 VoiceOver Labels

```swift
// Exercise row
ExerciseRowView(exercise: exercise)
    .accessibilityLabel("\(exercise.name), \(exercise.muscleGroup.displayName), \(exercise.sets) séries, \(exercise.reps) repetições")

// Status badge
Image(systemName: "checkmark.circle.fill")
    .accessibilityLabel("Completo")

// Progress
Text("3/8 exercícios")
    .accessibilityLabel("3 de 8 exercícios completos")
```

### 6.2 Dynamic Type Support

```swift
// Use scalable fonts
.font(.body) // Will scale with system settings

// Limit scaling for specific elements
.font(.caption)
.dynamicTypeSize(.xSmall ... .large)
```

### 6.3 Color Contrast

- Ensure all text has sufficient contrast (4.5:1 minimum)
- Use system colors that adapt to accessibility settings
- Don't rely solely on color to convey information

---

## 7. Implementation Guidelines

### 7.1 File Organization

```
TreinoDuFuturo/
├── App/
│   ├── TreinoDuFuturoApp.swift
│   └── ContentView.swift
│
├── Models/
│   ├── WorkoutPlan.swift
│   ├── Exercise.swift
│   ├── WorkoutSession.swift
│   ├── ExerciseSet.swift
│   ├── CheckIn.swift
│   └── Enums/
│       ├── MuscleGroup.swift
│       └── ExerciseType.swift
│
├── Views/
│   ├── Home/
│   │   └── HomeView.swift
│   │
│   ├── Workout/
│   │   ├── WorkoutsTabView.swift
│   │   ├── Plans/
│   │   │   ├── WorkoutPlanListView.swift
│   │   │   ├── WorkoutPlanRowView.swift
│   │   │   ├── WorkoutPlanDetailView.swift
│   │   │   ├── CreateWorkoutPlanView.swift
│   │   │   └── EditWorkoutPlanView.swift
│   │   │
│   │   ├── Exercises/
│   │   │   ├── AddExerciseView.swift
│   │   │   ├── ExerciseRowView.swift
│   │   │   ├── SelectExerciseSourceView.swift
│   │   │   └── SelectExistingExerciseView.swift
│   │   │
│   │   ├── Library/
│   │   │   ├── ExerciseLibraryView.swift
│   │   │   └── ExerciseLibraryRow.swift
│   │   │
│   │   └── Execute/
│   │       ├── ExecuteWorkoutView.swift
│   │       ├── ExecuteExerciseView.swift
│   │       ├── ExerciseExecutionRow.swift
│   │       ├── RestTimerView.swift
│   │       └── WorkoutSummaryView.swift
│   │
│   ├── Progress/
│   │   ├── ProgressView.swift
│   │   ├── WorkoutHistoryListView.swift
│   │   ├── WorkoutHistoryRowView.swift
│   │   ├── SessionDetailView.swift
│   │   ├── MuscleGroupListView.swift
│   │   ├── MuscleGroupExercisesView.swift
│   │   └── ExerciseHistoryView.swift
│   │
│   ├── CheckIn/
│   │   ├── CheckInView.swift
│   │   ├── RegisterCheckInView.swift
│   │   ├── ViewAllCheckInsView.swift
│   │   ├── MonthlyCalendarView.swift
│   │   └── CheckInDayCell.swift
│   │
│   └── Components/
│       ├── PrimaryButton.swift
│       ├── SecondaryButton.swift
│       ├── EmptyStateView.swift
│       ├── ValidationTextField.swift
│       ├── MuscleGroupTag.swift
│       ├── CircularProgressView.swift
│       ├── StatCard.swift
│       └── ProgressHeader.swift
│
├── ViewModels/
│   ├── HomeViewModel.swift
│   ├── WorkoutPlanListViewModel.swift
│   ├── CreateWorkoutPlanViewModel.swift
│   ├── WorkoutPlanDetailViewModel.swift
│   ├── EditWorkoutPlanViewModel.swift
│   ├── AddExerciseViewModel.swift
│   ├── ExerciseLibraryViewModel.swift
│   ├── WorkoutSessionViewModel.swift
│   ├── ExecuteExerciseViewModel.swift
│   ├── RestTimerViewModel.swift
│   ├── WorkoutSummaryViewModel.swift
│   ├── ProgressViewModel.swift
│   ├── CheckInViewModel.swift
│   ├── CalendarViewModel.swift
│   └── RegisterCheckInViewModel.swift
│
├── Utilities/
│   ├── Extensions/
│   │   ├── Date+Extensions.swift
│   │   ├── Calendar+Extensions.swift
│   │   └── UIImage+Compression.swift
│   │
│   └── Helpers/
│       ├── ImagePicker.swift
│       └── HapticManager.swift
│
└── Resources/
    └── Assets.xcassets/
```

### 7.2 Implementation Order

**Phase 1: Foundation**
1. Set up project structure
2. Create SwiftData models
3. Create enums (MuscleGroup, ExerciseType)
4. Implement ContentView with TabView

**Phase 2: Core Components**
5. Create all reusable components (PrimaryButton, EmptyStateView, etc.)
6. Create date extensions

**Phase 3: Workout Plans**
7. WorkoutPlanListView + ViewModel
8. CreateWorkoutPlanView + AddExerciseView
9. WorkoutPlanDetailView
10. EditWorkoutPlanView

**Phase 4: Workout Execution**
11. ExecuteWorkoutView + ViewModel
12. ExecuteExerciseView + ViewModel
13. RestTimerView + ViewModel
14. WorkoutSummaryView

**Phase 5: Home & Check-In**
15. HomeView + ViewModel
16. CheckInView + Calendar
17. RegisterCheckInView

**Phase 6: Progress**
18. ProgressView with tabs
19. WorkoutHistoryListView
20. MuscleGroupListView + related views

**Phase 7: Polish**
21. Exercise Library
22. Animations and transitions
23. Accessibility improvements

### 7.3 Key SwiftUI Patterns

```swift
// State management in views
@State private var isShowingSheet = false
@State private var searchQuery = ""

// Environment and Query
@Environment(\.modelContext) private var modelContext
@Environment(\.dismiss) private var dismiss
@Query(sort: \WorkoutPlan.modifiedDate, order: .reverse) private var plans: [WorkoutPlan]

// ViewModel integration
@State private var viewModel = SomeViewModel()

// Form validation pattern
var isFormValid: Bool {
    !name.isEmpty && sets > 0 && reps > 0
}

// Conditional navigation
NavigationLink(value: destination) {
    RowContent()
}
.navigationDestination(for: DestinationType.self) { destination in
    DestinationView(item: destination)
}
```

### 7.4 Localization (Portuguese - Brazil)

All user-facing strings should be in Portuguese:

```swift
// Navigation titles
"Home"
"Treinos"
"Progresso"
"Check-in"

// Actions
"Salvar"
"Cancelar"
"Editar"
"Apagar"
"Adicionar"
"Criar"
"Iniciar Treino"
"Finalizar Treino"
"Fazer Check-in"

// Labels
"Nome do Plano"
"Descrição"
"Séries"
"Repetições"
"Descanso"
"Peso"
"Título"
"Calorias"
"Local"
"Data e Hora"

// Status
"ATIVO"
"Completo"
"Em Andamento"
"Pendente"

// Empty states
"Nenhum plano criado"
"Nenhum exercício adicionado"
"Nenhum treino realizado"
"Sua biblioteca está vazia"

// Relative time
"Há X minutos"
"Há X horas"
"Há X dias"
"Há X semanas"
```

---

## Summary

This UI/UX specification provides a complete blueprint for implementing the NaNuca fitness app using SwiftUI and iOS 17+ features. The design follows Apple's Human Interface Guidelines while providing a clean, functional interface for workout management.

**Key Technical Requirements**:
- iOS 17.0+
- SwiftUI
- SwiftData for persistence
- MVVM architecture with @Observable
- Native components (no external dependencies)

**Design Principles**:
- Clean, minimalist interface
- Consistent spacing and typography
- Native iOS patterns (lists, forms, navigation)
- Accessible design with VoiceOver support
- Dark mode compatible (system colors)

Use this document as a reference to implement each screen, ensuring consistency across the entire application.
