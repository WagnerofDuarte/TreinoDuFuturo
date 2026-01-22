# NaNuca - Implementation Roadmap

**Version**: 1.0  
**Created**: January 22, 2026  
**Based on**: AppDocumentation.md

---

## Overview

This roadmap outlines the phased implementation plan for the NaNuca iOS fitness app. The project is divided into **8 phases** with an estimated total development time of **6-8 weeks** for a single developer.

---

## Phase Summary

| Phase | Name | Duration | Priority | Dependencies |
|-------|------|----------|----------|--------------|
| 1 | Foundation & Core Setup | 3-4 days | P0 | None |
| 2 | Data Models (SwiftData) | 3-4 days | P0 | Phase 1 |
| 3 | Workout Plan Management | 5-6 days | P1 | Phase 2 |
| 4 | Workout Execution | 6-7 days | P1 | Phase 3 |
| 5 | Home Dashboard | 2-3 days | P1 | Phase 4 |
| 6 | Check-In System | 4-5 days | P1 | Phase 2 |
| 7 | Progress Tracking | 4-5 days | P2 | Phase 4 |
| 8 | Polish & Testing | 3-4 days | P2 | All phases |

**Total Estimated Duration**: 30-38 days (~6-8 weeks)

---

## Phase 1: Foundation & Core Setup

**Duration**: 3-4 days  
**Priority**: P0 (Critical)  
**Goal**: Set up project structure, dependencies, and basic navigation

### Tasks

#### 1.1 Project Configuration
- [ ] Create new Xcode project (iOS 17.0+, SwiftUI lifecycle)
- [ ] Configure `Info.plist`:
  - Add `NSCameraUsageDescription`
  - Add `NSPhotoLibraryUsageDescription`
- [ ] Set up asset catalog with accent color
- [ ] Configure app icon placeholder

#### 1.2 Folder Structure
- [ ] Create folder hierarchy:
  ```
  NaNuca/
  ├── Models/
  ├── Views/
  │   ├── Home/
  │   ├── Workout/
  │   ├── Progress/
  │   ├── CheckIn/
  │   └── Components/
  ├── ViewModels/
  └── Utilities/
      ├── Extensions/
      └── Helpers/
  ```

#### 1.3 App Entry Point
- [ ] Configure `NaNucaApp.swift` with ModelContainer
- [ ] Create root `ContentView.swift` with TabView structure:
  - Home tab
  - Treinos tab
  - Progresso tab
  - Check-in tab

#### 1.4 Base Components
- [ ] Create `PrimaryButton.swift` component
- [ ] Create `EmptyStateView.swift` component
- [ ] Create `ValidationFeedback.swift` component

#### 1.5 Utility Extensions
- [ ] Create `Date+Extensions.swift` (relative time formatting)
- [ ] Create `UIImage+Compression.swift` (photo compression)

### Deliverables
- ✅ Working app shell with 4 tabs
- ✅ Project structure organized
- ✅ Base reusable components ready

---

## Phase 2: Data Models (SwiftData)

**Duration**: 3-4 days  
**Priority**: P0 (Critical)  
**Goal**: Define all SwiftData models and relationships

### Tasks

#### 2.1 MuscleGroup Enum
- [ ] Create `MuscleGroup.swift`:
  - 7 cases: chest, back, legs, shoulders, arms, abs, cardio
  - Portuguese localized display names
  - `tagColor` computed property
  - `iconName` computed property (SF Symbols)
  - Conform to `Codable`, `CaseIterable`

#### 2.2 WorkoutPlan Model
- [ ] Create `WorkoutPlan.swift` with `@Model`:
  - `id: UUID` (unique)
  - `name: String`
  - `desc: String`
  - `isActive: Bool`
  - `createdDate: Date`
  - `modifiedDate: Date`
  - `exercises: [Exercise]` relationship (cascade delete)
  - `init()` method with defaults

#### 2.3 Exercise Model
- [ ] Create `Exercise.swift` with `@Model`:
  - `id: UUID` (unique)
  - `name: String`
  - `muscleGroup: MuscleGroup`
  - `sets: Int`, `reps: Int`, `restSeconds: Int`
  - `videoURL: String?`
  - `order: Int`
  - `plan: WorkoutPlan?` relationship (nullify)
  - `exerciseSets: [ExerciseSet]` relationship

#### 2.4 WorkoutSession Model
- [ ] Create `WorkoutSession.swift` with `@Model`:
  - `id: UUID` (unique)
  - `startDate: Date`, `endDate: Date?`
  - `isCompleted: Bool`
  - `planId: UUID`, `planName: String` (denormalized)
  - `exerciseSets: [ExerciseSet]` relationship (cascade)
  - `duration` computed property

#### 2.5 ExerciseSet Model
- [ ] Create `ExerciseSet.swift` with `@Model`:
  - `id: UUID` (unique)
  - `exerciseId: UUID`, `exerciseName: String`, `muscleGroup: MuscleGroup`
  - `setNumber: Int`, `weight: Double?`, `reps: Int`
  - `completedDate: Date`, `notes: String?`
  - `session: WorkoutSession?`, `exercise: Exercise?` relationships

#### 2.6 CheckIn Model
- [ ] Create `CheckIn.swift` with `@Model`:
  - `id: UUID` (unique)
  - `date: Date`, `photoData: Data?`
  - `exerciseType: String`, `title: String`
  - `calories: Int?`, `location: String?`, `notes: String`
  - `workoutSession: WorkoutSession?` relationship

#### 2.7 ExerciseType Utility
- [ ] Create `ExerciseType.swift`:
  - Enum with predefined check-in types
  - Cases: Run, Gym, Swim, Bike, Walk, Yoga, Cycling, Strength Training
  - Icon names and colors

### Deliverables
- ✅ All 5 SwiftData models created
- ✅ Relationships configured with proper delete rules
- ✅ Enums with localized values

---

## Phase 3: Workout Plan Management

**Duration**: 5-6 days  
**Priority**: P1 (High)  
**Goal**: Complete CRUD operations for workout plans and exercises

### Tasks

#### 3.1 ViewModels
- [ ] Create `WorkoutPlanListViewModel.swift`:
  - Search query management
  - Filter logic
  - Delete plan method
  
- [ ] Create `CreateWorkoutPlanViewModel.swift`:
  - Form state (name, description)
  - Validation logic
  - Save method
  
- [ ] Create `WorkoutPlanDetailViewModel.swift`:
  - Toggle active state
  - Delete plan method
  - State for sheets/alerts
  
- [ ] Create `EditWorkoutPlanViewModel.swift`:
  - Pre-populate form
  - Update plan method
  
- [ ] Create `AddExerciseViewModel.swift`:
  - Exercise form state
  - Validation logic
  - Add to plan/library method

#### 3.2 List & Row Views
- [ ] Create `WorkoutPlanListView.swift`:
  - NavigationStack
  - @Query for plans
  - Search bar
  - Empty state
  - Swipe to delete
  
- [ ] Create `WorkoutPlanRowView.swift`:
  - Plan name, exercise count
  - "ATIVO" badge
  - Relative time

#### 3.3 Detail View
- [ ] Create `WorkoutPlanDetailView.swift`:
  - Plan info header
  - Exercise list
  - "Iniciar Treino" button
  - Toolbar: Edit, Activate, Delete

#### 3.4 Create & Edit Views
- [ ] Create `CreateWorkoutPlanView.swift`:
  - Form with validation
  - Add exercise button
  - Save/Cancel actions
  
- [ ] Create `EditWorkoutPlanView.swift`:
  - Pre-filled form
  - Reorder exercises
  - Delete exercises

#### 3.5 Exercise Views
- [ ] Create `AddExerciseView.swift`:
  - Exercise form fields
  - Muscle group picker
  - Steppers for sets/reps/rest
  - Optional video URL
  - Save to library toggle

- [ ] Create `ExerciseRowView.swift`:
  - Exercise name
  - Muscle group tag (colored)
  - Sets × Reps format

### Deliverables
- ✅ Create, read, update, delete workout plans
- ✅ Add/remove exercises from plans
- ✅ Search and filter plans
- ✅ Activate/deactivate plans

---

## Phase 4: Workout Execution

**Duration**: 6-7 days  
**Priority**: P1 (High)  
**Goal**: Full workout session execution with timers and tracking

### Tasks

#### 4.1 Session ViewModel
- [ ] Create `WorkoutSessionViewModel.swift`:
  - Check for existing incomplete sessions
  - Start new session
  - Resume existing session
  - Abandon and start new
  - Calculate progress
  - Finalize session

#### 4.2 Execute Workout View
- [ ] Create `ExecuteWorkoutView.swift`:
  - List exercises with status badges
  - Progress header
  - "Finalizar Treino" button
  - Exercise navigation

#### 4.3 Execute Exercise ViewModel & View
- [ ] Create `ExecuteExerciseViewModel.swift`:
  - Current set tracking
  - Input validation (weight/reps)
  - Fetch last workout data
  - Save set method
  
- [ ] Create `ExecuteExerciseView.swift`:
  - Last workout data display
  - Weight/reps input fields
  - Real-time validation
  - Save set button

- [ ] Create `ExerciseExecutionRow.swift`:
  - Set number badge
  - Completed set display
  - Input area for current set

#### 4.4 Rest Timer
- [ ] Create `RestTimerViewModel.swift`:
  - Countdown logic (Combine Timer)
  - Pause/resume/skip
  - Haptic feedback trigger
  - Audio feedback trigger
  
- [ ] Create `RestTimerView.swift`:
  - Circular progress indicator
  - Countdown display
  - Control buttons
  
- [ ] Create `CircularProgressView.swift`:
  - Animated arc
  - Configurable colors/width

#### 4.5 Workout Summary
- [ ] Create `WorkoutSummaryViewModel.swift`:
  - Calculate duration
  - Count exercises/sets/reps
  
- [ ] Create `WorkoutSummaryView.swift`:
  - Summary stats display
  - "Concluir" button

#### 4.6 Status Components
- [ ] Create `ProgressHeader.swift`:
  - Progress text
  - Progress bar

#### 4.7 Background Timer Support
- [ ] Implement background timer continuation (3 min max)
- [ ] Handle app state changes

### Deliverables
- ✅ Complete workout execution flow
- ✅ Automatic rest timer with feedback
- ✅ Incremental set saving
- ✅ Session resume/abandon logic
- ✅ Workout summary display

---

## Phase 5: Home Dashboard

**Duration**: 2-3 days  
**Priority**: P1 (High)  
**Goal**: Central dashboard with quick actions

### Tasks

#### 5.1 Home ViewModel
- [ ] Create `HomeViewModel.swift`:
  - Fetch active plan
  - Fetch last workout session
  - Fetch today's check-in
  - Format display data

#### 5.2 Home View
- [ ] Create `HomeView.swift`:
  - Greeting section
  - Current date
  - Check-in status card
  - Active plan card
  - Last workout card
  - Quick action navigation

#### 5.3 Home Cards
- [ ] Check-in card:
  - Conditional display (done/not done)
  - "Fazer Check-in" button
  
- [ ] Active plan card:
  - Plan name
  - "Iniciar Treino" button
  - Empty state message
  
- [ ] Last workout card:
  - Plan name
  - Relative time
  - Duration

### Deliverables
- ✅ Dashboard with real-time data
- ✅ Quick actions to other features
- ✅ Automatic updates on data changes

---

## Phase 6: Check-In System

**Duration**: 4-5 days  
**Priority**: P1 (High)  
**Goal**: Photo check-ins with calendar visualization

### Tasks

#### 6.1 ViewModels
- [ ] Create `CheckInViewModel.swift`:
  - Calculate streaks
  - Load monthly data
  - Get check-ins for specific day
  
- [ ] Create `CalendarViewModel.swift`:
  - Generate calendar grid
  - Track months with check-ins
  - Navigate between months
  
- [ ] Create `RegisterCheckInViewModel.swift`:
  - Form state management
  - Photo selection handling
  - Image compression
  - Validation
  - Save check-in

#### 6.2 Register Check-In
- [ ] Create `RegisterCheckInView.swift`:
  - Exercise type picker
  - Title field
  - Photo picker button
  - Optional fields (calories, location)
  - Date picker
  - Validation feedback

#### 6.3 Photo Handling
- [ ] Implement camera access (UIImagePickerController wrapper)
- [ ] Implement photo library access (PHPicker wrapper)
- [ ] Handle permission requests
- [ ] Implement photo compression utility

#### 6.4 Calendar Views
- [ ] Create `CheckInView.swift`:
  - Summary section (total count, streaks)
  - Current month calendar
  - "View All" button
  
- [ ] Create `MonthlyCalendarView.swift`:
  - Month/year header
  - 7-column grid layout
  - Day cells
  
- [ ] Create `CheckInDayCell.swift`:
  - Day number
  - Photo thumbnail (if exists)
  - Exercise type icon (if no photo)

#### 6.5 Historical View
- [ ] Create `ViewAllCheckInsView.swift`:
  - Scrollable list of months
  - Only months with check-ins
  - Calendar for each month

#### 6.6 Streak Logic
- [ ] Create `Calendar+CheckIn.swift`:
  - Calculate current streak
  - Calculate best streak
  - Monthly statistics

### Deliverables
- ✅ Register check-ins with photos
- ✅ Calendar visualization
- ✅ Streak tracking
- ✅ Historical navigation

---

## Phase 7: Progress Tracking

**Duration**: 4-5 days  
**Priority**: P2 (Medium)  
**Goal**: Workout history and exercise analytics

### Tasks

#### 7.1 Progress ViewModel
- [ ] Create `ProgressViewModel.swift`:
  - Load workout history
  - Load exercise history
  - Group by muscle group
  - Calculate personal records

#### 7.2 Workout History
- [ ] Create `ProgressView.swift`:
  - Segmented control (Treinos | Exercícios)
  - Tab content switching
  
- [ ] Create `WorkoutHistoryListView.swift`:
  - List completed sessions
  - Sort by date descending
  - Empty state
  
- [ ] Create `WorkoutHistoryRowView.swift`:
  - Date/time
  - Plan name
  - Duration

#### 7.3 Session Detail
- [ ] Create `SessionDetailView.swift`:
  - Session metadata
  - List of exercises
  - Sets grouped by exercise

#### 7.4 Exercise History
- [ ] Create `MuscleGroupListView.swift`:
  - 7 muscle group cards
  - Icons and colors
  
- [ ] Create `MuscleGroupExercisesView.swift`:
  - Exercises in selected group
  - Last execution date
  - Total executions
  
- [ ] Create `ExerciseHistoryView.swift`:
  - Personal record
  - Statistics
  - All sets list

#### 7.5 Data Structures
- [ ] Create `ExerciseStats` struct:
  - Exercise info
  - Aggregated metrics
  - Set history

### Deliverables
- ✅ Workout session history
- ✅ Session detail view
- ✅ Exercise history by muscle group
- ✅ Personal records display

---

## Phase 8: Polish & Testing

**Duration**: 3-4 days  
**Priority**: P2 (Medium)  
**Goal**: Refine UX, fix bugs, and ensure quality

### Tasks

#### 8.1 Exercise Library (P2 Feature)
- [ ] Create `WorkoutsTabView.swift` with segmented control
- [ ] Create `ExerciseLibraryView.swift`
- [ ] Create `ExerciseLibraryRow.swift`
- [ ] Create `AddExerciseToLibraryView.swift`
- [ ] Create `SelectExerciseSourceView.swift`
- [ ] Create `SelectExistingExerciseView.swift`
- [ ] Implement copy exercise from library to plan

#### 8.2 UI Polish
- [ ] Consistent color scheme across app
- [ ] Proper loading states
- [ ] Error handling with user-friendly messages
- [ ] Animations and transitions
- [ ] Dark mode support verification

#### 8.3 Edge Cases
- [ ] Handle incomplete sessions properly
- [ ] Prevent duplicate taps on save buttons
- [ ] Handle photo permission denial gracefully
- [ ] Validate all user inputs

#### 8.4 Performance
- [ ] Test with 50+ workout plans
- [ ] Test with 100+ sessions
- [ ] Test with 12+ months of check-ins
- [ ] Optimize @Query fetch limits

#### 8.5 Testing
- [ ] Test all CRUD operations
- [ ] Test cascade delete behavior
- [ ] Test workout execution flow
- [ ] Test check-in with/without photos
- [ ] Test on multiple device sizes

### Deliverables
- ✅ Exercise library feature
- ✅ Polished UI/UX
- ✅ All edge cases handled
- ✅ Performance verified

---

## Implementation Order Summary

### Week 1-2
1. **Phase 1**: Foundation & Core Setup
2. **Phase 2**: Data Models (SwiftData)

### Week 3-4
3. **Phase 3**: Workout Plan Management
4. **Phase 4**: Workout Execution (start)

### Week 5
5. **Phase 4**: Workout Execution (complete)
6. **Phase 5**: Home Dashboard

### Week 6-7
7. **Phase 6**: Check-In System
8. **Phase 7**: Progress Tracking

### Week 8
9. **Phase 8**: Polish & Testing

---

## Risk Mitigation

| Risk | Mitigation |
|------|------------|
| SwiftData learning curve | Start with simple models, add complexity gradually |
| Background timer limitations | Accept 3-minute background limit, document for users |
| Photo storage size | Implement aggressive compression, test with many photos |
| Complex workout execution flow | Build incrementally, test each component |
| Calendar calculations | Use Date extension utilities, handle edge cases |

---

## Success Metrics

- [ ] All 6 main features implemented
- [ ] App runs smoothly on iOS 17+ devices
- [ ] No crashes during normal usage
- [ ] Data persists correctly between sessions
- [ ] Photos compress to acceptable sizes
- [ ] Rest timer works reliably

---

## Future Enhancements (Post-MVP)

These features are documented but not included in the initial roadmap:

1. **Cloud Sync** - iCloud synchronization
2. **Widgets** - Home screen widgets for quick check-in
3. **Apple Watch** - Companion app for workout tracking
4. **Export Data** - Export workout history to CSV/PDF
5. **Localization** - Multiple language support
6. **Apple Health** - Integration with HealthKit

---

## 📚 Swift Learning Topics by Task

This section maps each task to the Swift/iOS topics a junior developer should study to complete it.

### Phase 1: Foundation & Core Setup

| Task | Swift Topics to Learn |
|------|----------------------|
| **1.1 Project Configuration** | Xcode project setup, Info.plist, Privacy descriptions, Asset catalogs |
| **1.2 Folder Structure** | Swift module organization, Access control (`public`, `private`), Naming conventions |
| **1.3 App Entry Point** | `@main`, `App` protocol, `Scene`, ModelContainer, TabView, SF Symbols, `@State` |
| **1.4 Base Components** | Custom Views, ViewModifiers, `@Binding`, Generics, ButtonStyle |
| **1.5 Utility Extensions** | Extensions, DateFormatter, RelativeDateTimeFormatter, UIImage manipulation |

### Phase 2: Data Models (SwiftData)

| Task | Swift Topics to Learn |
|------|----------------------|
| **2.1 MuscleGroup Enum** | Enumerations, CaseIterable, Codable, Computed properties, Switch statements |
| **2.2 WorkoutPlan Model** | SwiftData `@Model` macro, UUID, Relationships, Cascade delete rules |
| **2.3 Exercise Model** | Inverse relationships, Optional types (`?`), Nullify delete rule |
| **2.4 WorkoutSession Model** | Denormalization, Computed properties, Date arithmetic, Optional chaining |
| **2.5 ExerciseSet Model** | Complex relationships, Double type, Data modeling |
| **2.6 CheckIn Model** | Binary Data storage, Optional relationships, Large data handling |
| **2.7 ExerciseType Utility** | Static properties, SF Symbols naming, Color schemes |

### Phase 3: Workout Plan Management

| Task | Swift Topics to Learn |
|------|----------------------|
| **3.1 ViewModels** | MVVM architecture, `@Observable` macro, `@Published`, Dependency injection, Form validation |
| **3.2 List & Row Views** | NavigationStack, `@Query` macro, Predicate, SortDescriptor, List, ForEach, `.swipeActions`, `.searchable` |
| **3.3 Detail View** | `navigationDestination`, Toolbar, Sheets, Alerts, `@Environment`, `dismiss` |
| **3.4 Create & Edit Views** | Form, TextField, TextEditor, `@FocusState`, `@Bindable` |
| **3.5 Exercise Views** | Picker, Stepper, Section, Toggle, URL validation, Keyboard types |

### Phase 4: Workout Execution

| Task | Swift Topics to Learn |
|------|----------------------|
| **4.1 Session ViewModel** | State machines, Complex predicates, Transaction handling, Error handling (`do-catch`, `throws`) |
| **4.2 Execute Workout View** | Progress tracking, Dynamic lists, Programmatic navigation |
| **4.3 Execute Exercise Views** | Input binding, NumberFormatter, Historical data queries, Real-time validation |
| **4.4 Rest Timer** | **Combine framework** (`Timer.publish`), Haptic feedback, Audio feedback, Animation, Custom shapes with `Path` |
| **4.5 Workout Summary** | Data aggregation, `reduce()` function, Statistics calculation |
| **4.6 Status Components** | ProgressView, GeometryReader, Custom progress bars |
| **4.7 Background Timer** | `scenePhase`, Background tasks, UserDefaults, NotificationCenter, State preservation |

### Phase 5: Home Dashboard

| Task | Swift Topics to Learn |
|------|----------------------|
| **5.1 Home ViewModel** | Multiple queries, Computed display data, Reactive updates |
| **5.2 Home View** | ScrollView, VStack/HStack, Spacer, Date formatting |
| **5.3 Home Cards** | Card UI pattern (shadows, corners), Conditional views, NavigationLink, `@ViewBuilder` |

### Phase 6: Check-In System

| Task | Swift Topics to Learn |
|------|----------------------|
| **6.1 ViewModels** | Date calculations, Calendar API, Dictionary grouping, Month navigation |
| **6.2 Register Check-In** | Segmented Picker, DatePicker, Optional field handling |
| **6.3 Photo Handling** | **PhotosPicker**, **UIViewControllerRepresentable**, Camera/Photo permissions, Image compression, Async/Await |
| **6.4 Calendar Views** | LazyVGrid, GridItem, Calendar calculations (days in month, first weekday) |
| **6.5 Historical View** | LazyVStack, Grouping by month, Lazy loading |
| **6.6 Streak Logic** | Algorithm design, Set operations, Date normalization |

### Phase 7: Progress Tracking

| Task | Swift Topics to Learn |
|------|----------------------|
| **7.1 Progress ViewModel** | Data aggregation, Personal records (max values), Custom sort comparators, `filter`, `map` |
| **7.2 Workout History** | Segmented control, `@State` for tabs, List sections |
| **7.3 Session Detail** | Detail views, Grouped display, Nested ForEach |
| **7.4 Exercise History** | Card grid layout, Multi-level navigation, Statistics display |
| **7.5 Data Structures** | Custom structs, Identifiable protocol, Value types vs Reference types |

### Phase 8: Polish & Testing

| Task | Swift Topics to Learn |
|------|----------------------|
| **8.1 Exercise Library** | Feature organization, Deep copying objects, Library pattern |
| **8.2 UI Polish** | Color schemes, `preferredColorScheme`, Loading states, Transitions, Animation curves |
| **8.3 Edge Cases** | Guard statements, Debouncing, Permission handling, Input sanitization |
| **8.4 Performance** | Instruments app, Lazy loading, Fetch limits, Memory management (ARC) |
| **8.5 Testing** | **XCTest**, `@testable import`, In-memory ModelContainer, UI Testing, Async testing |

---

## 📖 Complete Swift Topics Reference

### 🟢 Fundamentals (Phase 1-2)

#### Swift Language Basics
- **Variables & Constants**: `var`, `let`, type inference
- **Data Types**: `String`, `Int`, `Double`, `Bool`, `Date`, `UUID`, `Data`
- **Optionals**: `?`, `!`, optional binding (`if let`, `guard let`), nil coalescing (`??`), optional chaining (`?.`)
- **Collections**: `Array`, `Dictionary`, `Set`
- **Control Flow**: `if-else`, `switch`, `for-in`, `while`
- **Functions**: Parameters, return types, default values, closures

#### Enumerations
- Basic enum declaration with `case`
- Raw values and associated values
- `CaseIterable` protocol for iteration
- `Codable` conformance for persistence
- Computed properties in enums
- Pattern matching with `switch`

#### Extensions
- Adding methods to existing types
- Computed properties in extensions
- Protocol conformance via extensions
- Organizing code with extensions

#### Access Control
- `public`, `internal`, `private`, `fileprivate`
- Module boundaries
- Best practices for encapsulation

### 🔵 SwiftUI Essentials (Phase 1-5)

#### View Protocol & Body
- `View` protocol conformance
- `some View` opaque return type
- `@ViewBuilder` for conditional content

#### Layout Containers
- `VStack`, `HStack`, `ZStack`
- `Spacer`, `Divider`
- `ScrollView`
- `List` and `ForEach`
- `LazyVStack`, `LazyHStack`, `LazyVGrid`
- `GeometryReader`
- `GridItem` and grid layouts

#### Common Views
- `Text`, `Image`, `Button`
- `TextField`, `TextEditor`, `SecureField`
- `Toggle`, `Picker`, `Stepper`, `Slider`
- `DatePicker`
- `ProgressView`
- `Form`, `Section`

#### View Modifiers
- `.padding()`, `.frame()`, `.background()`
- `.foregroundColor()`, `.font()`
- `.cornerRadius()`, `.shadow()`
- `.overlay()`, `.clipShape()`
- Custom `ViewModifier` creation

#### State Management
- `@State` - Local view state
- `@Binding` - Two-way binding
- `@Environment` - Environment values
- `@FocusState` - Keyboard focus

#### Navigation
- `NavigationStack` (iOS 16+)
- `NavigationLink` and `navigationDestination`
- `TabView` with tab items
- `.sheet()`, `.fullScreenCover()`
- `.alert()`, `.confirmationDialog()`
- `dismiss` environment action

#### Lists & Data Display
- `List` with static and dynamic content
- `ForEach` with `Identifiable`
- `.swipeActions()` modifier
- `.searchable()` modifier
- Empty states handling

### 🟣 SwiftData (Phase 2-7)

#### Model Definition
- `@Model` macro
- `@Attribute` for property configuration
- `@Relationship` for connections
- Unique constraints

#### Relationships
- One-to-one, one-to-many, many-to-many
- Delete rules: `.cascade`, `.nullify`, `.deny`
- Inverse relationships

#### Querying
- `@Query` macro in SwiftUI views
- `#Predicate` for filtering
- `SortDescriptor` for ordering
- Fetch limits and pagination

#### Context Operations
- `ModelContext` for CRUD
- `insert()`, `delete()`
- Saving changes
- In-memory containers for testing

### 🟠 MVVM Architecture (Phase 3-7)

#### Observable Pattern
- `@Observable` macro (iOS 17+)
- `@ObservableObject` and `@Published` (iOS 14+)
- `@Bindable` for binding to observable objects

#### ViewModel Responsibilities
- Business logic separation
- Form state management
- Validation logic
- Data transformation for views

#### Dependency Injection
- Passing `ModelContext` to ViewModels
- Environment-based injection
- Constructor injection

### 🔴 Combine Framework (Phase 4)

#### Publishers
- `Timer.publish()` for countdown timers
- `CurrentValueSubject`, `PassthroughSubject`
- Publisher operators: `map`, `filter`, `sink`

#### Subscriptions
- `sink()` for receiving values
- `store(in:)` with `AnyCancellable`
- Cancellation handling

### 🟡 UIKit Integration (Phase 6)

#### UIViewControllerRepresentable
- Wrapping `UIImagePickerController`
- Coordinator pattern
- `makeUIViewController`, `updateUIViewController`

#### PhotosPicker (SwiftUI)
- `PhotosPicker` view
- `PhotosPickerItem`
- Loading images asynchronously

#### Permissions
- `AVCaptureDevice.requestAccess(for:)`
- `PHPhotoLibrary.requestAuthorization()`
- Handling permission states

#### Image Handling
- `UIImage` and `Image` conversion
- `jpegData(compressionQuality:)`
- Async image loading

### 🟤 Advanced Topics (Phase 4, 7-8)

#### Async/Await
- `async` functions
- `await` keyword
- `Task` for launching async work
- `@MainActor` for UI updates

#### Error Handling
- `throws` and `throw`
- `do-catch` blocks
- `Result` type
- Custom error types

#### Date & Calendar
- `Date`, `DateComponents`
- `Calendar.current`
- `DateFormatter`, `RelativeDateTimeFormatter`
- Date arithmetic and comparisons

#### Haptics & Audio
- `UIImpactFeedbackGenerator`
- `UINotificationFeedbackGenerator`
- `AudioServicesPlaySystemSound`

#### Animation
- `withAnimation {}`
- `.animation()` modifier
- Animation types: `.easeInOut`, `.spring()`
- `.transition()` for view transitions

#### Custom Drawing
- `Shape` protocol
- `Path` for custom shapes
- Animated arcs and circles

### 🧪 Testing (Phase 8)

#### XCTest Framework
- `XCTestCase` subclass
- `@testable import`
- `setUp()` and `tearDown()`
- Assertions: `XCTAssertEqual`, `XCTAssertTrue`, `XCTAssertNil`

#### SwiftData Testing
- In-memory `ModelContainer`
- Test data fixtures
- Testing CRUD operations

#### UI Testing
- `XCUIApplication`
- Accessibility identifiers
- Element queries and interactions

#### Async Testing
- `XCTestExpectation`
- `wait(for:timeout:)`
- Testing async functions

### 📱 App Lifecycle (Phase 4, 8)

#### Scene Phase
- `@Environment(\.scenePhase)`
- `.active`, `.inactive`, `.background`
- Responding to state changes

#### State Preservation
- `UserDefaults` for simple data
- Saving/restoring timer state
- Handling app termination

---

## 🎯 Learning Path Summary

```
Week 1-2 (Phase 1-2):
├── Swift Basics (Variables, Optionals, Enums)
├── SwiftUI Fundamentals (Views, State, Layout)
└── SwiftData (Models, Relationships)

Week 3-4 (Phase 3-4):
├── MVVM Architecture
├── Navigation & Forms
├── Combine (Timers)
└── Animation

Week 5-6 (Phase 5-6):
├── Complex Queries
├── UIKit Integration
├── Photo Handling
└── Calendar Calculations

Week 7-8 (Phase 7-8):
├── Data Aggregation
├── Performance Optimization
└── Testing (XCTest)
```

---

**Document Version**: 1.1  
**Last Updated**: January 22, 2026
