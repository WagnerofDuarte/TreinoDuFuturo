# NaNuca - Complete Technical Documentation

**Version**: 1.0  
**Last Updated**: January 21, 2026  
**Platform**: iOS 17.0+  
**Language**: Swift 5.9+

---

## Table of Contents

1. [App Overview & Purpose](#1-app-overview--purpose)
2. [Required Knowledge & Learning Topics](#2-required-knowledge--learning-topics)
3. [Technical Architecture](#3-technical-architecture)
4. [Data Models](#4-data-models)
5. [Feature Specifications](#5-feature-specifications)
6. [User Interface Components](#6-user-interface-components)
7. [ViewModels & Business Logic](#7-viewmodels--business-logic)
8. [Navigation & Flow](#8-navigation--flow)
9. [Validation Rules](#9-validation-rules)
10. [User Flows & Scenarios](#10-user-flows--scenarios)
11. [Success Criteria & Testing](#11-success-criteria--testing)
12. [Future Enhancements](#12-future-enhancements)

---

## 1. App Overview & Purpose

### 1.1 Introduction

**NaNuca** is a native iOS fitness management application designed to help users organize, execute, and track their workout routines. The app provides a complete solution for gym enthusiasts who want to:

- Manually create custom workout plans with exercises organized by muscle groups
- Execute workout sessions with real-time tracking of sets, weights, and repetitions
- Use automatic rest timers with haptic and audio feedback between sets
- Register daily check-ins with photos to track consistency and motivation
- View comprehensive progress analytics and workout history
- Maintain a global exercise library for reuse across multiple workout plans

### 1.2 Target Users

- Gym-goers and fitness enthusiasts who follow structured training programs
- Athletes tracking their strength training progress
- Individuals who prefer manual control over their workout planning
- Users who value visual tracking of their fitness journey through photos

### 1.3 Core Value Propositions

1. **Complete Workout Management**: From planning to execution to analysis
2. **Real-time Execution Support**: Rest timers, last workout data, progress indicators
3. **Motivation Through Tracking**: Check-in streaks, calendar visualization, progress metrics
4. **Flexibility**: Global exercise library, customizable plans, optional metrics
5. **Native iOS Experience**: Fast, offline-first, follows iOS design patterns

### 1.4 Key Differentiators

- **Manual Control**: Users define everything - no pre-built programs or AI suggestions
- **Exercise Library**: Reusable exercises across multiple plans without duplication
- **Visual Check-ins**: Photo-based calendar for motivational tracking
- **Background Rest Timer**: Continues working even when app is minimized (up to 3 minutes)
- **Incomplete Session Handling**: Resume or abandon previous unfinished workouts

---

## 2. Required Knowledge & Learning Topics

To successfully recreate this application, a developer needs to master the following topics:

### 2.1 Swift Language Fundamentals

#### Core Swift
- **Swift 5.9+ Syntax**: Variables, constants, optionals, optional binding (if let, guard let)
- **Swift Types**: Structs, Classes, Enums (raw values, associated values, CaseIterable)
- **Protocols**: Protocol-oriented programming, protocol conformance, Codable, Identifiable
- **Collections**: Arrays, Dictionaries, Sets, and their methods (filter, map, reduce, sorted)
- **Error Handling**: do-try-catch, throws, Result type
- **Closures**: Syntax, capturing values, trailing closure syntax, @escaping
- **Property Wrappers**: @State, @Binding, @Observable, @Environment, @Query, @Relationship
- **Generics**: Generic functions and types
- **Concurrency**: async/await basics (for future features)
- **Access Control**: private, fileprivate, internal, public

#### Advanced Swift Features
- **Value Types vs Reference Types**: When to use struct vs class
- **Copy-on-Write**: Understanding Swift's memory optimization
- **Weak and Unowned References**: Avoiding retain cycles
- **Type Casting**: as?, as!, is operator
- **Extensions**: Adding functionality to existing types
- **Computed Properties**: get, set, willSet, didSet
- **String Interpolation**: \(variable) syntax
- **Conditional Compilation**: #if DEBUG

### 2.2 SwiftUI Framework

#### SwiftUI Basics
- **Declarative Syntax**: How SwiftUI differs from UIKit
- **View Protocol**: Creating custom views
- **View Modifiers**: Chaining modifiers, order matters
- **Layout System**: VStack, HStack, ZStack, Spacer, Divider
- **State Management**: @State, @Binding, @Observable (iOS 17+)
- **Lists**: List, ForEach, Section, ScrollView
- **Forms**: Form, TextField, TextEditor, Picker, Toggle, Stepper
- **Navigation**: NavigationStack, NavigationLink, toolbar, navigationTitle
- **Sheets and Alerts**: .sheet, .alert, .confirmationDialog
- **Buttons and Controls**: Button, Menu, DatePicker

#### Advanced SwiftUI
- **Custom Modifiers**: ViewModifier protocol
- **PreferenceKeys**: Cross-view communication
- **GeometryReader**: Reading view dimensions
- **@Environment**: EnvironmentValues, modelContext, dismiss
- **Animations**: withAnimation, .animation modifier, transitions
- **Gestures**: onTapGesture, swipe gestures, drag and drop
- **TabView**: Creating tabbed interfaces
- **SearchableModifier**: .searchable for search bars
- **Conditional Views**: if-else, switch in ViewBuilder
- **ViewBuilder**: Understanding the @ViewBuilder attribute
- **EmptyState Handling**: ContentUnavailableView (iOS 17+)

### 2.3 SwiftData Framework (iOS 17+)

#### SwiftData Fundamentals
- **@Model Macro**: Defining data models
- **@Attribute**: Unique constraints, custom attributes
- **@Relationship**: One-to-many, many-to-one relationships
- **Delete Rules**: .cascade, .nullify, .deny
- **ModelContainer**: Setting up the data container
- **ModelContext**: Performing CRUD operations
- **@Query Property Wrapper**: Fetching data in SwiftUI views
- **FetchDescriptor**: Building complex queries with predicates and sorting
- **Predicate Macros**: #Predicate for type-safe filtering
- **SortDescriptor**: Ordering query results
- **Transactions**: Understanding save() and rollback()
- **Schema Evolution**: Handling model changes (migrations)

#### Data Persistence Patterns
- **CRUD Operations**: insert, delete, save context
- **Cascade Deletes**: When to use .cascade vs .nullify
- **Prefetching**: relationshipKeyPathsForPrefetching for performance
- **FetchLimit**: Limiting query results for performance
- **Computed Properties**: Derived data that isn't stored
- **Data Validation**: Model-level validation logic

### 2.4 iOS Development Concepts

#### Foundation Framework
- **Date and DateFormatter**: Working with dates and times
- **UUID**: Generating unique identifiers
- **UserDefaults**: Simple key-value storage (if needed)
- **FileManager**: Managing files and directories (for photos)
- **Data**: Binary data handling (image compression)
- **Timer**: Scheduled timers (rest timer)
- **NotificationCenter**: Observing system events

#### UIKit Integration
- **UIImage**: Image manipulation and compression
- **UIImagePickerController**: Camera and photo library access (UIViewControllerRepresentable)
- **PHPickerViewController**: Modern photo picker
- **UIViewControllerRepresentable**: Wrapping UIKit in SwiftUI
- **Image Compression**: JPEG compression for efficient storage

#### System Integration
- **Permissions**: Camera and photo library authorization (AVFoundation, Photos framework)
- **Info.plist**: Configuring app capabilities and permissions descriptions
- **Background Modes**: Background audio and timer execution
- **Haptic Feedback**: UIImpactFeedbackGenerator, UINotificationFeedbackGenerator
- **Audio Playback**: AVFoundation for sound effects (AudioServicesPlaySystemSound)
- **App Lifecycle**: scenePhase, applicationWillTerminate

### 2.5 Combine Framework

#### Combine Basics (for Rest Timer)
- **Publishers**: Timer.publish for scheduled events
- **Subscribers**: sink, assign
- **Operators**: map, filter, debounce
- **AnyCancellable**: Managing subscriptions and memory
- **Published Property**: @Published for observable properties (legacy, pre-@Observable)

### 2.6 Architectural Patterns

#### MVVM Pattern
- **Model**: Data structures and business entities
- **View**: SwiftUI views (UI layer)
- **ViewModel**: Observable business logic, state management, no UI code
- **Separation of Concerns**: Keeping UI logic out of models, data logic out of views
- **Testability**: Why MVVM improves testability

#### Design Patterns
- **Observer Pattern**: State changes triggering UI updates
- **Delegate Pattern**: Protocol-based callbacks (UIImagePickerControllerDelegate)
- **Strategy Pattern**: Different behaviors (exercise types, muscle groups)
- **Factory Pattern**: Creating objects based on configuration
- **Singleton Pattern**: Shared instances (if needed for managers)

### 2.7 Xcode and iOS Development Tools

#### Xcode IDE
- **Project Navigator**: Managing files and folders
- **Scheme Configuration**: Build settings, targets
- **Asset Catalog**: Managing images and colors
- **Info.plist**: App configuration
- **Signing & Capabilities**: App ID, provisioning profiles
- **SwiftUI Previews**: Canvas preview and interactive previews
- **Simulator**: Testing on virtual devices
- **Debugging**: Breakpoints, console logging, print statements
- **Instruments**: Performance profiling (optional)

#### Version Control
- **Git Basics**: commit, branch, merge, pull, push
- **.gitignore**: Excluding build artifacts and user-specific files
- **Feature Branches**: Branch-based development workflow

### 2.8 App Architecture & Organization

#### Project Structure
- **Folder Organization**: Models, Views, ViewModels, Utilities, Extensions
- **File Naming Conventions**: Consistent naming patterns
- **Code Organization**: Extensions for grouping related functionality
- **Documentation**: Code comments, MARK: comments
- **Modularity**: Reusable components and utilities

### 2.9 User Experience Design

#### iOS Design Patterns
- **Navigation Patterns**: Tab bars, navigation stacks, modals
- **Form Design**: Grouped lists, pickers, input validation
- **Empty States**: Meaningful messages and calls-to-action
- **Feedback**: Loading indicators, error messages, success confirmations
- **Accessibility**: VoiceOver labels (basic understanding)
- **Dark Mode**: Supporting both light and dark appearances

#### UI/UX Best Practices
- **Native iOS Conventions**: Following Apple's Human Interface Guidelines
- **Consistent Styling**: Reusable button styles, color schemes
- **Visual Hierarchy**: Proper use of font sizes, weights, spacing
- **Touch Targets**: Minimum 44x44pt for tappable elements
- **Safe Areas**: Respecting device notches and home indicators

### 2.10 Data Management & Performance

#### Performance Optimization
- **Lazy Loading**: Loading data only when needed
- **Prefetching**: Loading related data efficiently
- **Pagination**: Limiting query results (fetchLimit)
- **Image Optimization**: Compressing photos before storage
- **Memory Management**: Understanding ARC (Automatic Reference Counting)
- **View Lifecycle**: Understanding when views are created/destroyed

#### Data Validation
- **Input Validation**: Real-time validation of user inputs
- **Required Fields**: Enforcing mandatory data
- **Data Constraints**: Min/max values, character limits
- **Error Messages**: User-friendly validation feedback

### 2.11 Testing Fundamentals (Optional but Recommended)

- **Unit Testing**: XCTest framework basics
- **Testing ViewModels**: Testing business logic in isolation
- **Test-Driven Development**: Writing tests before implementation
- **Mock Data**: Creating sample data for testing

### 2.12 Debugging & Troubleshooting

- **Reading Error Messages**: Understanding compiler errors and warnings
- **Console Logging**: Using print() and Logger for debugging
- **Breakpoints**: Pausing execution to inspect state
- **Common SwiftUI Issues**: Understanding view update cycles, binding issues
- **SwiftData Debugging**: Inspecting database state, understanding fetch results
- **Memory Leaks**: Detecting retain cycles with weak/unowned

### 2.13 Localization Basics (Current App is Portuguese)

- **String Localization**: NSLocalizedString basics
- **Date Formatting**: Locale-aware date formatting
- **Number Formatting**: Decimal separators, currency formatting
- **RTL Support**: Right-to-left language considerations (future)

### 2.14 Additional Topics

- **Regular Expressions**: Pattern matching (if needed for validation)
- **Calendar Calculations**: Working with Calendar for check-in streaks
- **Date Arithmetic**: Adding days, comparing dates
- **Time Zone Handling**: Understanding local vs UTC dates
- **Codable**: JSON encoding/decoding (for future sync features)

---

## 3. Technical Architecture

### 3.1 Technology Stack

| Component | Technology | Version |
|-----------|-----------|---------|
| Language | Swift | 5.9+ |
| UI Framework | SwiftUI | iOS 17.0+ |
| Data Persistence | SwiftData | iOS 17.0+ |
| Architecture | MVVM | - |
| Concurrency | Combine (Timers) | - |
| Media | AVFoundation | For audio feedback |
| Photos | PhotosUI | For photo picker |

### 3.2 Design Pattern: MVVM

```
┌─────────────────────────────────────┐
│            View (SwiftUI)           │
│  ┌──────────────────────────────┐  │
│  │  WorkoutPlanListView         │  │
│  │  ExecuteWorkoutView          │  │
│  │  CheckInView                 │  │
│  └──────────────────────────────┘  │
└──────────────┬──────────────────────┘
               │ Observes
               │ @State, @Binding
               ▼
┌─────────────────────────────────────┐
│       ViewModel (@Observable)        │
│  ┌──────────────────────────────┐  │
│  │  WorkoutPlanListViewModel    │  │
│  │  WorkoutSessionViewModel     │  │
│  │  CheckInViewModel            │  │
│  └──────────────────────────────┘  │
└──────────────┬──────────────────────┘
               │ Reads/Writes
               │ ModelContext
               ▼
┌─────────────────────────────────────┐
│        Model (SwiftData)            │
│  ┌──────────────────────────────┐  │
│  │  @Model WorkoutPlan          │  │
│  │  @Model Exercise             │  │
│  │  @Model WorkoutSession       │  │
│  │  @Model ExerciseSet          │  │
│  │  @Model CheckIn              │  │
│  └──────────────────────────────┘  │
└─────────────────────────────────────┘
```

**Responsibilities:**

- **View**: Displays UI, handles user interactions, no business logic
- **ViewModel**: Contains business logic, manages state, performs data operations, no UI code
- **Model**: Defines data structures, relationships, and persistence rules

### 3.3 Project Structure

```
NaNuca/
├── NaNucaApp.swift          # App entry point, ModelContainer setup
├── ContentView.swift               # TabView with 4 main tabs
│
├── Models/                         # SwiftData @Model entities
│   ├── WorkoutPlan.swift           # Workout plan entity
│   ├── Exercise.swift              # Exercise entity
│   ├── WorkoutSession.swift        # Workout execution session
│   ├── ExerciseSet.swift           # Individual set record
│   ├── CheckIn.swift               # Daily check-in record
│   └── MuscleGroup.swift           # Enum for muscle groups
│
├── Views/                          # SwiftUI views
│   ├── Home/
│   │   └── HomeView.swift          # Dashboard with quick actions
│   ├── Workout/
│   │   ├── WorkoutsTabView.swift   # Wrapper for Plans + Library tabs
│   │   ├── WorkoutPlanListView.swift
│   │   ├── WorkoutPlanDetailView.swift
│   │   ├── WorkoutPlanRowView.swift
│   │   ├── CreateWorkoutPlanView.swift
│   │   ├── EditWorkoutPlanView.swift
│   │   ├── AddExerciseView.swift
│   │   ├── ExerciseLibraryView.swift
│   │   ├── AddExerciseToLibraryView.swift
│   │   ├── SelectExerciseSourceView.swift
│   │   ├── SelectExistingExerciseView.swift
│   │   └── Execute/                # Workout execution views
│   │       ├── ExecuteWorkoutView.swift
│   │       ├── ExecuteExerciseView.swift
│   │       ├── ExerciseExecutionRow.swift
│   │       ├── WorkoutSummaryView.swift
│   │       └── RestTimerView.swift
│   ├── Progress/
│   │   ├── ProgressView.swift      # Tabbed view: Workouts + Exercises
│   │   ├── WorkoutHistoryListView.swift
│   │   ├── WorkoutHistoryRowView.swift
│   │   ├── SessionDetailView.swift
│   │   ├── ExerciseHistoryListView.swift
│   │   ├── ExerciseHistoryView.swift
│   │   ├── MuscleGroupListView.swift
│   │   └── MuscleGroupExercisesView.swift
│   ├── CheckIn/
│   │   ├── CheckInView.swift       # Calendar view with summary
│   │   ├── RegisterCheckInView.swift
│   │   ├── ViewAllCheckInsView.swift
│   │   ├── MonthlyCalendarView.swift
│   │   └── CheckInDayCell.swift
│   └── Components/                 # Reusable UI components
│       ├── PrimaryButton.swift
│       ├── EmptyStateView.swift
│       ├── ExerciseRowView.swift
│       ├── ExerciseLibraryRow.swift
│       ├── ProgressHeader.swift
│       ├── SetInputView.swift
│       ├── ValidationFeedback.swift
│       └── CircularProgressView.swift
│
├── ViewModels/                     # Business logic (@Observable)
│   ├── HomeViewModel.swift
│   ├── WorkoutPlanListViewModel.swift
│   ├── WorkoutPlanDetailViewModel.swift
│   ├── CreateWorkoutPlanViewModel.swift
│   ├── EditWorkoutPlanViewModel.swift
│   ├── AddExerciseViewModel.swift
│   ├── ExerciseLibraryViewModel.swift
│   ├── ProgressViewModel.swift
│   ├── CheckInViewModel.swift
│   ├── CalendarViewModel.swift
│   ├── RegisterCheckInViewModel.swift
│   └── Execute/
│       ├── WorkoutSessionViewModel.swift
│       ├── ExecuteExerciseViewModel.swift
│       ├── WorkoutSummaryViewModel.swift
│       └── RestTimerViewModel.swift
│
└── Utilities/
    ├── ExerciseType.swift          # Enum for check-in exercise types
    ├── Extensions/
    │   ├── Date+Extensions.swift   # Relative time formatting
    │   ├── Calendar+Extensions.swift
    │   ├── Calendar+CheckIn.swift  # Check-in specific calendar logic
    │   └── UIImage+Compression.swift
    └── Helpers/
        └── Logger.swift            # Logging utility (optional)
```

### 3.4 Data Flow

```
User Interaction (View)
        ↓
ViewModel Method Call
        ↓
Business Logic Execution
        ↓
SwiftData ModelContext Operations
        ↓
Database Update (SQLite)
        ↓
@Query Property Wrapper Updates
        ↓
View Automatically Re-renders
```

### 3.5 Dependency Management

**No External Dependencies**: The app uses only native iOS frameworks:
- Foundation
- SwiftUI
- SwiftData
- AVFoundation (audio feedback)
- PhotosUI (photo picker)
- UIKit (image handling, UIViewControllerRepresentable bridges)
- Combine (timer publishers)

### 3.6 App Entry Point

**NaNucaApp.swift**:
```swift
@main
struct NaNucaApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
        .modelContainer(for: [
            WorkoutPlan.self,
            Exercise.self,
            WorkoutSession.self,
            ExerciseSet.self,
            CheckIn.self
        ])
    }
}
```

**ContentView.swift** (Root TabView):
```swift
struct ContentView: View {
    var body: some View {
        TabView {
            HomeView()
                .tabItem { Label("Home", systemImage: "house.fill") }
            
            WorkoutsTabView()
                .tabItem { Label("Treinos", systemImage: "dumbbell.fill") }
            
            ProgressView()
                .tabItem { Label("Progresso", systemImage: "chart.bar.fill") }
            
            CheckInView()
                .tabItem { Label("Check-in", systemImage: "calendar") }
        }
    }
}
```

---

## 4. Data Models

### 4.1 Entity Relationship Diagram

```
┌─────────────────────────────┐
│       WorkoutPlan           │
│─────────────────────────────│
│ id: UUID                    │
│ name: String                │
│ desc: String?               │
│ isActive: Bool              │
│ createdDate: Date           │
│ modifiedDate: Date          │
└──────────┬──────────────────┘
           │ 1
           │ has many (cascade delete)
           │ *
┌──────────▼──────────────────┐
│         Exercise            │
│─────────────────────────────│
│ id: UUID                    │
│ name: String                │
│ muscleGroup: MuscleGroup    │
│ sets: Int                   │
│ reps: Int                   │
│ restSeconds: Int            │
│ videoURL: String?           │
│ order: Int                  │
└──────────┬──────────────────┘
           │ 1
           │ references
           │ *
┌──────────▼──────────────────┐       ┌─────────────────────────────┐
│     WorkoutSession          │       │        CheckIn              │
│─────────────────────────────│       │─────────────────────────────│
│ id: UUID                    │       │ id: UUID                    │
│ startDate: Date             │◄──────│ date: Date                  │
│ endDate: Date?              │ 0..1  │ photoData: Data?            │
│ isCompleted: Bool           │       │ exerciseType: String        │
│ duration: TimeInterval      │       │ title: String               │
└──────────┬──────────────────┘       │ calories: Int?              │
           │ 1                         │ location: String?           │
           │ has many (cascade)        │ notes: String               │
           │ *                         └─────────────────────────────┘
┌──────────▼──────────────────┐
│       ExerciseSet           │
│─────────────────────────────│
│ id: UUID                    │
│ setNumber: Int              │
│ weight: Double?             │
│ reps: Int                   │
│ completedDate: Date         │
│ notes: String?              │
└─────────────────────────────┘

┌─────────────────────────────┐
│       MuscleGroup (Enum)    │
│─────────────────────────────│
│ chest                       │
│ back                        │
│ legs                        │
│ shoulders                   │
│ arms                        │
│ abs                         │
│ cardio                      │
└─────────────────────────────┘
```

### 4.2 Model Specifications

#### 4.2.1 WorkoutPlan

**Purpose**: Represents a workout plan containing multiple exercises.

```swift
@Model
final class WorkoutPlan {
    @Attribute(.unique) var id: UUID
    var name: String
    var desc: String
    var isActive: Bool
    var createdDate: Date
    var modifiedDate: Date
    
    @Relationship(deleteRule: .cascade, inverse: \Exercise.plan)
    var exercises: [Exercise]
    
    init(name: String, desc: String = "", isActive: Bool = false)
}
```

**Attributes**:
- `id`: Unique identifier (UUID)
- `name`: Plan name (required, max 100 chars)
- `desc`: Optional description
- `isActive`: Whether this is the currently active plan (only one can be active)
- `createdDate`: Timestamp when plan was created
- `modifiedDate`: Timestamp of last modification

**Relationships**:
- `exercises`: One-to-many with Exercise (cascade delete - deleting plan deletes its exercises)

**Business Rules**:
- Only one plan can have `isActive = true` at a time
- When a plan is activated, all other plans are deactivated
- Deleting an active plan doesn't auto-activate another plan
- Empty plans (0 exercises) are allowed

#### 4.2.2 Exercise

**Purpose**: Represents a single exercise with its configuration.

```swift
@Model
final class Exercise {
    @Attribute(.unique) var id: UUID
    var name: String
    var muscleGroup: MuscleGroup
    var sets: Int
    var reps: Int
    var restSeconds: Int
    var videoURL: String?
    var order: Int
    
    @Relationship(deleteRule: .nullify)
    var plan: WorkoutPlan?
    
    @Relationship(deleteRule: .nullify, inverse: \ExerciseSet.exercise)
    var exerciseSets: [ExerciseSet]
    
    init(name: String, muscleGroup: MuscleGroup, sets: Int = 3, 
         reps: Int = 12, restSeconds: Int = 60, order: Int = 0)
}
```

**Attributes**:
- `id`: Unique identifier
- `name`: Exercise name (required, max 100 chars)
- `muscleGroup`: One of 7 muscle groups (enum)
- `sets`: Default number of sets (min: 1, default: 3)
- `reps`: Default number of reps (min: 1, default: 12)
- `restSeconds`: Rest time between sets in seconds (default: 60)
- `videoURL`: Optional URL to exercise tutorial video
- `order`: Position in the workout plan

**Relationships**:
- `plan`: Optional many-to-one with WorkoutPlan (null means global library exercise)
- `exerciseSets`: One-to-many with ExerciseSet (nullify delete - sets remain if exercise deleted)

**Business Rules**:
- If `plan` is nil, exercise is in global library
- If `plan` is set, exercise belongs to that specific plan
- Can be copied from library to plan (creates new Exercise instance)
- Must have at least 1 set and 1 rep

#### 4.2.3 WorkoutSession

**Purpose**: Records an executed workout session.

```swift
@Model
final class WorkoutSession {
    @Attribute(.unique) var id: UUID
    var startDate: Date
    var endDate: Date?
    var isCompleted: Bool
    var planId: UUID
    var planName: String
    
    @Relationship(deleteRule: .cascade, inverse: \ExerciseSet.session)
    var exerciseSets: [ExerciseSet]
    
    var duration: TimeInterval {
        guard let endDate else { return 0 }
        return endDate.timeIntervalSince(startDate)
    }
    
    init(planId: UUID, planName: String, startDate: Date = Date())
}
```

**Attributes**:
- `id`: Unique identifier
- `startDate`: When workout started
- `endDate`: When workout ended (nil if in progress)
- `isCompleted`: Whether session was formally completed
- `planId`: Reference to WorkoutPlan UUID (denormalized)
- `planName`: Snapshot of plan name at execution time (denormalized)

**Relationships**:
- `exerciseSets`: One-to-many with ExerciseSet (cascade delete)

**Computed Properties**:
- `duration`: Calculated time between start and end

**Business Rules**:
- Only one incomplete session per plan should exist
- When starting new workout, check for existing incomplete sessions
- Sessions can be incomplete but still have sets saved (incremental save)
- Deleting a plan doesn't delete its historical sessions

#### 4.2.4 ExerciseSet

**Purpose**: Records a single set execution within a workout session.

```swift
@Model
final class ExerciseSet {
    @Attribute(.unique) var id: UUID
    var exerciseId: UUID
    var exerciseName: String
    var muscleGroup: MuscleGroup
    var setNumber: Int
    var weight: Double?
    var reps: Int
    var completedDate: Date
    var notes: String?
    
    @Relationship(deleteRule: .nullify)
    var session: WorkoutSession?
    
    @Relationship(deleteRule: .nullify)
    var exercise: Exercise?
    
    init(exerciseId: UUID, exerciseName: String, muscleGroup: MuscleGroup,
         setNumber: Int, weight: Double?, reps: Int)
}
```

**Attributes**:
- `id`: Unique identifier
- `exerciseId`: Reference to Exercise UUID (denormalized)
- `exerciseName`: Snapshot of exercise name (denormalized)
- `muscleGroup`: Snapshot of muscle group (denormalized)
- `setNumber`: Which set number (1, 2, 3, etc.)
- `weight`: Weight used in kg/lbs (nil = bodyweight)
- `reps`: Repetitions completed (min: 1)
- `completedDate`: Timestamp when set was finished
- `notes`: Optional notes about the set

**Relationships**:
- `session`: Many-to-one with WorkoutSession (nullify - historical data preserved)
- `exercise`: Many-to-one with Exercise (nullify - historical data preserved)

**Business Rules**:
- Weight can be nil (bodyweight exercises)
- Reps must be > 0
- Sets are saved immediately (incremental persistence)
- Historical data is denormalized to preserve what was actually done

#### 4.2.5 CheckIn

**Purpose**: Records daily check-ins with photos and training details.

```swift
@Model
final class CheckIn {
    @Attribute(.unique) var id: UUID
    var date: Date
    var photoData: Data?
    var exerciseType: String
    var title: String
    var calories: Int?
    var location: String?
    var notes: String
    
    @Relationship(deleteRule: .nullify)
    var workoutSession: WorkoutSession?
    
    init(date: Date = Date(), photoData: Data? = nil, 
         exerciseType: String, title: String)
}
```

**Attributes**:
- `id`: Unique identifier
- `date`: Date and time of check-in
- `photoData`: Compressed JPEG photo data (optional)
- `exerciseType`: One of predefined types (Run, Gym, Swim, etc.)
- `title`: Check-in title (required, max 100 chars)
- `calories`: Optional calories burned
- `location`: Optional location text (max 200 chars)
- `notes`: Optional notes

**Relationships**:
- `workoutSession`: Optional link to completed workout (nullify)

**Business Rules**:
- Only one check-in per day recommended (not enforced)
- Photos are compressed before storage (JPEG compression)
- Date must not be in the future
- Exercise type must be from predefined list
- If no photo, calendar shows exercise type icon placeholder

#### 4.2.6 MuscleGroup (Enum)

**Purpose**: Categorizes exercises by muscle group.

```swift
enum MuscleGroup: String, Codable, CaseIterable {
    case chest = "Peito"
    case back = "Costas"
    case legs = "Pernas"
    case shoulders = "Ombros"
    case arms = "Braços"
    case abs = "Abdômen"
    case cardio = "Cardio"
    
    var tagColor: String { /* UI color */ }
    var iconName: String { /* SF Symbol */ }
}
```

**Cases**:
- `chest`: Chest exercises (blue)
- `back`: Back exercises (green)
- `legs`: Leg exercises (purple)
- `shoulders`: Shoulder exercises (orange)
- `arms`: Arm exercises (red)
- `abs`: Core/abs exercises (yellow)
- `cardio`: Cardio exercises (pink)

**Properties**:
- `tagColor`: iOS system color name for UI tags
- `iconName`: SF Symbol icon name

---

## 5. Feature Specifications

### 5.1 Feature 1: Workout Plan Management

#### Overview
Allows users to create, view, edit, activate, and delete custom workout plans. Each plan contains multiple exercises organized by muscle groups.

#### User Stories

##### US1: Create Workout Plan Manually (Priority: P1)

**Description**: Users can create a new workout plan from scratch with a name, description, and exercises.

**Acceptance Criteria**:
1. User taps "+" button in WorkoutPlanListView
2. CreateWorkoutPlanView sheet appears
3. User enters plan name (required) and description (optional)
4. User can add exercises with:
   - Exercise name (required)
   - Muscle group selection (picker)
   - Sets (stepper, default: 3, min: 1)
   - Reps (stepper, default: 12, min: 1)
   - Rest time (stepper, default: 60 seconds)
   - Optional video URL
5. User can add multiple exercises to the plan
6. Validation prevents saving without plan name
7. Plan saves and appears in list immediately
8. Empty plans (0 exercises) are allowed

**ViewModel**: `CreateWorkoutPlanViewModel`
**Views**: `CreateWorkoutPlanView`, `AddExerciseView`

##### US2: List and View All Workout Plans (Priority: P1)

**Description**: Users see all their workout plans in a scrollable list with search capability.

**Acceptance Criteria**:
1. WorkoutPlanListView shows all plans ordered by modifiedDate (newest first)
2. Each plan row displays:
   - Plan name
   - Number of exercises
   - "ATIVO" badge if `isActive == true`
   - Relative time since last modification
3. Search bar filters plans by name or description
4. Empty state shown when no plans exist
5. ContentUnavailableView.search shown when search has no results
6. Swipe-to-delete removes plans with confirmation alert

**ViewModel**: `WorkoutPlanListViewModel`
**Views**: `WorkoutPlanListView`, `WorkoutPlanRowView`

##### US3: View Plan Details (Priority: P1)

**Description**: Users can view complete details of a specific plan and its exercises.

**Acceptance Criteria**:
1. Tapping a plan navigates to WorkoutPlanDetailView
2. Shows plan name, description, and creation date
3. Lists all exercises with:
   - Exercise name
   - Muscle group tag (colored)
   - Sets × Reps format (e.g., "4 × 10")
   - SF Symbol icon for muscle group
4. Toolbar provides "Editar", "Ativar/Desativar", and delete options
5. Prominent "Iniciar Treino" button at bottom
6. Empty state if plan has no exercises

**ViewModel**: `WorkoutPlanDetailViewModel`
**Views**: `WorkoutPlanDetailView`, `ExerciseRowView`

##### US4: Edit Existing Plan (Priority: P2)

**Description**: Users can modify plan name, description, add/remove exercises, and reorder them.

**Acceptance Criteria**:
1. Tapping "Editar" opens EditWorkoutPlanView sheet
2. All current values pre-populate the form
3. User can:
   - Change plan name and description
   - Add new exercises
   - Remove exercises via swipe-to-delete
   - Reorder exercises via drag-and-drop
4. "Salvar" button commits changes
5. "Cancelar" button discards all changes
6. Validation matches create validation
7. Changes reflect immediately in list and detail views

**ViewModel**: `EditWorkoutPlanViewModel`
**Views**: `EditWorkoutPlanView`

##### US5: Mark Plan as Active (Priority: P2)

**Description**: Users can mark one plan as "active" for quick access from Home.

**Acceptance Criteria**:
1. User taps "Ativar" in toolbar menu
2. Selected plan becomes active (`isActive = true`)
3. All other plans automatically become inactive
4. "ATIVO" badge appears in list row
5. Active plan appears on Home dashboard
6. User can "Desativar" to have no active plan
7. Only one plan can be active at a time

**ViewModel**: `WorkoutPlanDetailViewModel`
**Method**: `toggleActive()`

##### US6: Delete Plan (Priority: P3)

**Description**: Users can permanently delete a workout plan.

**Acceptance Criteria**:
1. Swipe-to-delete in list shows delete button
2. Confirmation alert appears: "Tem certeza que deseja deletar este plano?"
3. Deleting confirms and removes plan permanently
4. All associated exercises are cascade-deleted
5. Historical workout sessions are preserved
6. If deleted plan was active, no plan becomes active automatically
7. View dismisses after deletion in detail view

**ViewModel**: `WorkoutPlanDetailViewModel`, `WorkoutPlanListViewModel`

---

### 5.2 Feature 2: Exercise Library

#### Overview
Global library of exercises that can be reused across multiple workout plans without duplication. Users can create exercises directly in the library or save exercises to the library when adding them to plans.

#### User Stories

##### US1: Manage Global Exercise Library (Priority: P2)

**Description**: Users access a global library of exercises independent of specific plans.

**Acceptance Criteria**:
1. WorkoutsTabView has segmented control: "Planos" | "Biblioteca"
2. Selecting "Biblioteca" shows ExerciseLibraryView
3. Exercises grouped by muscle group
4. Each exercise shows:
   - Name
   - Sets × Reps
   - Optional video icon
5. "+" button adds new exercise to library
6. Swipe-to-delete removes from library
7. Search and filter by muscle group
8. Empty state when library is empty

**ViewModel**: `ExerciseLibraryViewModel`
**Views**: `WorkoutsTabView`, `ExerciseLibraryView`, `ExerciseLibraryRow`

##### US2: Reuse Library Exercises in Plans (Priority: P2)

**Description**: Users can add exercises from the library to plans without duplicating data.

**Acceptance Criteria**:
1. In WorkoutPlanDetailView, tapping "+" shows SelectExerciseSourceView
2. Two options appear:
   - "Criar Novo Exercício"
   - "Usar Exercício Existente"
3. Selecting "Usar Exercício Existente" opens SelectExistingExerciseView
4. Shows all library exercises with search and filter
5. Selecting an exercise creates a copy in the plan
6. Copy is independent (modifying in plan doesn't affect library)
7. Original library exercise remains unchanged

**ViewModel**: `AddExerciseViewModel`, `WorkoutPlanDetailViewModel`
**Views**: `SelectExerciseSourceView`, `SelectExistingExerciseView`

##### US3: Save to Library When Creating (Priority: P2)

**Description**: When adding an exercise to a plan, users can optionally save it to the library simultaneously.

**Acceptance Criteria**:
1. AddExerciseView has `saveToLibrary` parameter
2. When `saveToLibrary = true`, creates two Exercise instances:
   - One linked to the plan
   - One in global library (plan = nil)
3. Both have same properties but independent IDs
4. Future edits to plan exercise don't affect library version

**ViewModel**: `AddExerciseViewModel`
**Method**: `addExercise(to:context:saveToLibrary:)`

---

### 5.3 Feature 3: Workout Execution

#### Overview
Complete workout execution flow with set tracking, rest timers, progress indicators, and session management.

#### User Stories

##### US1: Start and Complete Basic Workout Session (Priority: P1)

**Description**: Users can execute a workout plan, logging weights and reps for each set.

**Acceptance Criteria**:
1. "Iniciar Treino" button in WorkoutPlanDetailView or Home
2. Creates new WorkoutSession with startDate
3. ExecuteWorkoutView shows list of exercises from plan
4. Tapping an exercise opens ExecuteExerciseView
5. User inputs:
   - Weight (optional, decimal, bodyweight if empty)
   - Reps (required, integer > 0)
6. Real-time validation with inline error messages
7. Each set saves immediately to database
8. User can complete all exercises or partial workout
9. "Finalizar Treino" button ends session
10. WorkoutSummaryView shows:
    - Total duration
    - Exercises completed
    - Total sets and reps
11. Session marked `isCompleted = true`

**ViewModels**: `WorkoutSessionViewModel`, `ExecuteExerciseViewModel`, `WorkoutSummaryViewModel`
**Views**: `ExecuteWorkoutView`, `ExecuteExerciseView`, `ExerciseExecutionRow`, `WorkoutSummaryView`

##### US2: Automatic Rest Timer (Priority: P2)

**Description**: Timer starts automatically after completing a set (except last set).

**Acceptance Criteria**:
1. After confirming a set, timer starts automatically
2. Timer duration = exercise's `restSeconds` configuration
3. RestTimerView shows:
   - Circular progress animation
   - Countdown in seconds
   - Pause/Resume button
   - Skip button
4. When timer reaches 0:
   - Haptic feedback (vibration)
   - Brief sound notification (respects silent mode)
5. Timer continues in background for up to 3 minutes
6. If user starts next set before timer ends, timer auto-cancels
7. Last set of exercise doesn't trigger timer

**ViewModel**: `RestTimerViewModel`
**Views**: `RestTimerView`, `CircularProgressView`
**Technologies**: Combine (Timer.publish), AVFoundation (audio), UIImpactFeedbackGenerator

##### US3: View Last Workout Data (Priority: P2)

**Description**: During execution, users see their performance from the last completed session.

**Acceptance Criteria**:
1. ExecuteExerciseView fetches last workout data for current exercise
2. Displays "Último: 80kg × 10 reps" above input fields
3. Data comes from most recent completed session of same plan
4. If first time doing exercise, shows no data
5. Numbers formatted with locale (PT: "80,5 kg")
6. Users can reference but fields aren't auto-filled

**ViewModel**: `ExecuteExerciseViewModel`
**Method**: `fetchLastWorkoutData()`

##### US4: Visual Progress Tracking (Priority: P2)

**Description**: Users see which exercises are pending, in-progress, or completed during session.

**Acceptance Criteria**:
1. Each exercise in ExecuteWorkoutView has a status badge:
   - ⚪ Pendente (gray) - not started
   - 🟡 Em Andamento (yellow) - some sets done
   - ✅ Completo (green) - all recommended sets done
2. ProgressHeader shows: "3/8 exercícios completos"
3. Progress percentage calculated
4. Visual progress bar
5. User can manually mark exercise complete anytime
6. User can add more sets than configured amount

**ViewModel**: `WorkoutSessionViewModel`
**Computed Properties**: `exerciseStatus()`, `progressPercentage`, `progressText`
**Component**: `ProgressHeader`

##### US5: Handle Incomplete Sessions (Priority: P3)

**Description**: Detect and manage existing incomplete workout sessions.

**Acceptance Criteria**:
1. When starting a workout, check for existing incomplete session
2. If found, show alert:
   - "Você tem um treino em andamento"
   - "Retomar Treino" button
   - "Abandonar e Iniciar Novo" button
3. Retomar loads existing session with all saved sets
4. Abandonar marks old session as complete and starts new one
5. Incomplete sessions still save all sets (incremental persistence)
6. Sessions can be completed even if not all exercises done

**ViewModel**: `WorkoutSessionViewModel`
**Method**: `checkExistingSession()`

---

### 5.4 Feature 4: Home Dashboard

#### Overview
Central dashboard showing daily check-in status, active workout plan, and last workout summary.

#### User Stories

##### US1: Dashboard Overview (Priority: P1)

**Description**: Users see key information immediately upon opening the app.

**Acceptance Criteria**:
1. Greeting: "Olá, Atleta!"
2. Current date displayed
3. Check-in card:
   - If not done today: "Fazer Check-in" button
   - If done today: ✓ icon, "Check-in realizado!", timestamp
4. Active plan card:
   - If active plan exists: plan name, "Iniciar Treino" button
   - If no active plan: "Nenhum plano ativo" message
5. Last workout card:
   - Plan name
   - Relative time ("Há 2 dias")
   - Duration ("45 min")
   - If no workouts: hidden or "Nenhum treino realizado"
6. Tapping "Iniciar Treino" navigates to ExecuteWorkoutView
7. Tapping check-in button navigates to RegisterCheckInView

**ViewModel**: `HomeViewModel`
**Views**: `HomeView`

##### US2: Real-time Updates (Priority: P2)

**Description**: Dashboard updates automatically when data changes.

**Acceptance Criteria**:
1. After completing a workout, last workout card updates
2. After making a check-in, check-in card updates
3. After activating a plan, active plan card updates
4. Uses @Query for reactive updates
5. No manual refresh needed

**ViewModel**: `HomeViewModel`

---

### 5.5 Feature 5: Check-In System

#### Overview
Daily check-in tracking with photos, exercise types, and calendar visualization for consistency monitoring.

#### User Stories

##### US1: Quick Check-In Registration (Priority: P1)

**Description**: Users register daily check-ins with essential details and photos.

**Acceptance Criteria**:
1. "Check In" button on Home screen
2. RegisterCheckInView opens
3. Required fields:
   - Exercise type (picker): Run, Gym, Swim, Bike, Walk, Yoga, Cycling, Strength Training
   - Title (text field, max 100 chars)
4. Optional fields:
   - Photo (camera or gallery)
   - Calories burned (numeric)
   - Date & time (picker, defaults to now, no future dates)
   - Location (text, max 200 chars)
5. "Add Photo" button shows:
   - "Open Camera" option
   - "Choose from Gallery" option
6. Camera/gallery permissions requested if needed
7. Photo compressed to JPEG before storage
8. "Check In" button saves and returns to Home
9. Total check-in count increments

**ViewModel**: `RegisterCheckInViewModel`
**Views**: `RegisterCheckInView`
**Technologies**: PhotosUI (PHPickerViewController), UIImagePickerController for camera

##### US2: Monthly Calendar View (Priority: P1)

**Description**: Users see current month's check-ins displayed on a calendar with photos.

**Acceptance Criteria**:
1. CheckInView shows:
   - Summary section with total check-ins count
   - Current month calendar
2. Days with check-ins display:
   - Rounded training photo (if available)
   - Exercise type icon placeholder (if no photo)
3. Photo size: ~40-48pt, rounded
4. Multiple check-ins per day: show most recent photo
5. Calendar auto-updates after new check-in
6. Icons have distinct colors per exercise type

**ViewModel**: `CheckInViewModel`, `CalendarViewModel`
**Views**: `CheckInView`, `MonthlyCalendarView`, `CheckInDayCell`

##### US3: Historical Calendar Navigation (Priority: P2)

**Description**: Users browse all months containing check-ins.

**Acceptance Criteria**:
1. "View All Check-Ins" button below calendar
2. ViewAllCheckInsView opens
3. Vertical scrollable list of monthly calendars
4. Shows only months with at least one check-in
5. Ordered: current month at top, earliest at bottom
6. Each month displays check-in photos on appropriate days
7. Smooth scrolling through 12+ months

**ViewModel**: `CalendarViewModel`
**Views**: `ViewAllCheckInsView`

##### US4: Check-In Streaks (Priority: P2)

**Description**: Track consecutive check-in days for motivation.

**Acceptance Criteria**:
1. Calculate current streak (consecutive days with check-ins)
2. Track best streak (longest ever consecutive streak)
3. Display in CheckInView:
   - "🔥 Sequência Atual: 5 dias"
   - "⭐ Melhor Sequência: 14 dias"
4. Missing a day resets current streak to 0
5. Best streak persists even if current resets
6. Monthly statistics show "Check-ins: 18/31 (58%)"

**ViewModel**: `CheckInViewModel`
**Utility**: `Calendar+CheckIn.swift`

---

### 5.6 Feature 6: Progress Tracking

#### Overview
Comprehensive analytics showing workout history and exercise-specific progress.

#### User Stories

##### US1: Workout History List (Priority: P2)

**Description**: Users see all completed workout sessions.

**Acceptance Criteria**:
1. ProgressView has two tabs: "Treinos" | "Exercícios"
2. Treinos tab shows WorkoutHistoryListView
3. Lists all sessions where `isCompleted == true`
4. Ordered by startDate descending (most recent first)
5. Each row shows:
   - Start date and time
   - Plan name
   - Duration
   - Completion icon
6. Tapping row opens SessionDetailView
7. Empty state: "Nenhum treino realizado" with suggestion

**ViewModel**: `ProgressViewModel`
**Views**: `ProgressView`, `WorkoutHistoryListView`, `WorkoutHistoryRowView`

##### US2: Session Detail View (Priority: P2)

**Description**: Users see complete details of a specific workout session.

**Acceptance Criteria**:
1. SessionDetailView shows:
   - Session date and time
   - Plan name
   - Total duration
   - List of all exercises executed
2. For each exercise:
   - Exercise name and muscle group
   - All sets with weight × reps
3. Sets grouped by exercise
4. Formatted with locale (weight decimals)

**Views**: `SessionDetailView`

##### US3: Exercise History by Muscle Group (Priority: P3)

**Description**: Users browse exercises organized by muscle group and view individual exercise history.

**Acceptance Criteria**:
1. Exercícios tab shows MuscleGroupListView
2. 7 muscle group cards (Chest, Back, Legs, etc.)
3. Tapping group opens MuscleGroupExercisesView
4. Shows all exercises executed in that muscle group
5. Each exercise shows:
   - Name
   - Last execution date
   - Total times executed
6. Tapping exercise opens ExerciseHistoryView

**ViewModel**: `ProgressViewModel`
**Views**: `MuscleGroupListView`, `MuscleGroupExercisesView`

##### US4: Exercise-Specific Statistics (Priority: P3)

**Description**: Users see detailed stats and personal records for individual exercises.

**Acceptance Criteria**:
1. ExerciseHistoryView shows:
   - Exercise name
   - Personal record: "100kg × 8" (highest weight × reps at that weight)
   - Last execution date
   - Total sets ever completed
2. List of all sets for this exercise:
   - Date
   - Weight × Reps
   - Plan name
3. Sorted by date descending
4. Empty state if exercise never executed

**ViewModel**: `ProgressViewModel`
**Data Structure**: `ExerciseStats`
**Views**: `ExerciseHistoryView`

---

## 6. User Interface Components

### 6.1 Reusable Components

#### 6.1.1 PrimaryButton

**Purpose**: Consistent styled button for primary actions.

**Usage**:
```swift
PrimaryButton(title: "Salvar", systemImage: "checkmark") {
    viewModel.save()
}
```

**Properties**:
- `title`: Button text
- `systemImage`: Optional SF Symbol icon name
- `isEnabled`: Disabled state (default: true)
- `action`: Closure to execute on tap

**Styling**:
- Blue background (`.blue` or `.accent` color)
- White text
- Rounded corners (12pt radius)
- Full width with padding
- Disabled state: gray background, 0.6 opacity

#### 6.1.2 EmptyStateView

**Purpose**: Consistent empty state messaging with icon and call-to-action.

**Usage**:
```swift
EmptyStateView(
    icon: "dumbbell",
    title: "Nenhum plano criado",
    message: "Crie seu primeiro plano de treino",
    buttonTitle: "Criar Plano",
    action: { isShowingCreate = true }
)
```

**Properties**:
- `icon`: SF Symbol name
- `title`: Main message
- `message`: Descriptive subtitle
- `buttonTitle`: Optional action button text
- `action`: Optional button action closure

**Styling**:
- Centered vertically and horizontally
- Large icon (60-80pt)
- Gray/secondary text colors
- Spacious layout

#### 6.1.3 ExerciseRowView

**Purpose**: Display exercise in a list with muscle group tag.

**Usage**:
```swift
ExerciseRowView(exercise: exercise)
```

**Displays**:
- SF Symbol icon for muscle group
- Exercise name
- Colored tag with muscle group name
- "X × Y" format for sets and reps
- Video icon if videoURL exists

**Styling**:
- HStack layout
- Icon on left (colored by muscle group)
- Name and details in middle
- Tag on right
- Padding and divider

#### 6.1.4 ProgressHeader

**Purpose**: Show workout progress during execution.

**Usage**:
```swift
ProgressHeader(
    completedCount: 3,
    totalCount: 8,
    progressPercentage: 0.375
)
```

**Displays**:
- "3/8 exercícios completos"
- Progress bar (0-100%)
- Color changes based on progress (yellow → green)

#### 6.1.5 SetInputView

**Purpose**: Input fields for weight and reps with validation.

**Usage**:
```swift
SetInputView(
    weight: $weight,
    reps: $reps,
    isWeightValid: $isWeightValid,
    isRepsValid: $isRepsValid
)
```

**Features**:
- Two text fields: Weight (decimal), Reps (integer)
- Real-time validation on change
- Red border when invalid
- Placeholder: "Peso Corporal" for empty weight
- Number keyboard types

#### 6.1.6 ValidationFeedback

**Purpose**: Display inline validation error messages.

**Usage**:
```swift
ValidationFeedback(
    isValid: isRepsValid,
    message: "Repetições devem ser maior que zero"
)
```

**Styling**:
- Red text with warning icon
- Small font
- Only visible when `isValid == false`

#### 6.1.7 CircularProgressView

**Purpose**: Animated circular progress indicator for rest timer.

**Usage**:
```swift
CircularProgressView(
    progress: 0.66,
    lineWidth: 12,
    strokeColor: .blue
)
```

**Features**:
- Circular arc from top
- Animated progress changes
- Customizable line width and color
- Stroke cap: rounded

#### 6.1.8 RestTimerView

**Purpose**: Full rest timer interface with controls.

**Usage**:
```swift
RestTimerView(viewModel: restTimerViewModel)
```

**Displays**:
- CircularProgressView
- Countdown seconds in center
- Pause/Resume button
- Skip button
- Auto-dismiss on completion

**Interactions**:
- Tap pause to pause timer
- Tap resume to continue
- Tap skip to cancel and close
- Haptic and audio feedback at 0 seconds

---

## 7. ViewModels & Business Logic

### 7.1 ViewModel Principles

All ViewModels follow these principles:

1. **@Observable**: Use Swift's Observation framework (iOS 17+)
2. **No UI Code**: No SwiftUI imports, no view logic
3. **ModelContext Operations**: All database operations via passed ModelContext
4. **Validation**: Business logic validation before saving
5. **State Management**: Manage UI state (loading, errors, selections)
6. **Computed Properties**: Derive values from state

### 7.2 Key ViewModels

#### 7.2.1 WorkoutPlanListViewModel

**Responsibilities**:
- Manage search query
- Filter plans based on search
- Delete plans

**Properties**:
```swift
var searchQuery: String = ""
```

**Methods**:
```swift
func deletePlan(_ plan: WorkoutPlan, context: ModelContext)
func filteredPlans(_ allPlans: [WorkoutPlan]) -> [WorkoutPlan]
```

#### 7.2.2 CreateWorkoutPlanViewModel

**Responsibilities**:
- Manage plan creation form state
- Validate inputs
- Save new plan

**Properties**:
```swift
var planName: String = ""
var planDescription: String = ""
var errorMessage: String?
```

**Methods**:
```swift
func validate() -> Bool
func save(context: ModelContext) throws
```

**Validation Rules**:
- Plan name cannot be empty
- Plan name max 100 characters
- Description optional

#### 7.2.3 WorkoutPlanDetailViewModel

**Responsibilities**:
- Manage plan detail state
- Toggle active status
- Delete plan
- Manage exercise source selection

**Properties**:
```swift
var isShowingEdit: Bool = false
var isShowingAddExercise: Bool = false
var isShowingDeleteAlert: Bool = false
var isShowingSelectExerciseSource: Bool = false
```

**Methods**:
```swift
func toggleActive(plan: WorkoutPlan, context: ModelContext)
func deletePlan(_ plan: WorkoutPlan, context: ModelContext)
func deactivateAllPlans(except: UUID?, context: ModelContext)
```

**Business Logic**:
- `toggleActive()`: Sets plan.isActive, deactivates all other plans
- Only one plan can be active at a time

#### 7.2.4 AddExerciseViewModel

**Responsibilities**:
- Manage exercise creation form
- Validate exercise inputs
- Add to plan and/or library

**Properties**:
```swift
var exerciseName: String = ""
var selectedMuscleGroup: MuscleGroup = .chest
var sets: Int = 3
var reps: Int = 12
var restSeconds: Int = 60
var videoURL: String = ""
var errorMessage: String?
```

**Methods**:
```swift
func validate() -> Bool
func addExercise(to plan: WorkoutPlan?, context: ModelContext, saveToLibrary: Bool = false) throws
func addExerciseToLibrary(context: ModelContext) throws
```

**Validation Rules**:
- Exercise name required, max 100 chars
- Sets >= 1
- Reps >= 1
- RestSeconds >= 0
- VideoURL optional, valid URL format if provided

#### 7.2.5 WorkoutSessionViewModel

**Responsibilities**:
- Manage active workout session
- Check for existing incomplete sessions
- Save sets incrementally
- Calculate progress
- Finalize session

**Properties**:
```swift
var session: WorkoutSession?
var exercises: [Exercise] = []
var currentExerciseId: UUID?
var isShowingSummary: Bool = false
```

**Methods**:
```swift
func checkExistingSession(planId: UUID, context: ModelContext) -> WorkoutSession?
func startNewSession(plan: WorkoutPlan, context: ModelContext) throws
func resumeSession(_ session: WorkoutSession, context: ModelContext)
func abandonAndStartNew(plan: WorkoutPlan, context: ModelContext) throws
func saveSet(_ set: ExerciseSet, context: ModelContext) throws
func exerciseStatus(_ exercise: Exercise) -> ExerciseStatus
func progressPercentage() -> Double
func progressText() -> String
func finalizeSession(context: ModelContext) throws
```

**Business Logic**:
- Check for incomplete sessions before starting
- Sets save immediately (incremental persistence)
- Progress calculated from completed sets vs recommended sets
- Session can be finalized with incomplete exercises

#### 7.2.6 ExecuteExerciseViewModel

**Responsibilities**:
- Manage single exercise execution
- Validate set inputs
- Fetch last workout data
- Trigger rest timer

**Properties**:
```swift
var exercise: Exercise
var session: WorkoutSession
var currentSetNumber: Int = 1
var weight: String = ""
var reps: String = ""
var isWeightValid: Bool = true
var isRepsValid: Bool = true
var lastWorkoutData: LastWorkoutData?
var isShowingRestTimer: Bool = false
```

**Methods**:
```swift
func validateInputs() -> Bool
func saveSet(context: ModelContext) throws
func fetchLastWorkoutData(context: ModelContext)
func shouldShowRestTimer() -> Bool
```

**Validation Logic**:
- Weight: empty (bodyweight) or positive decimal
- Reps: required, positive integer > 0
- Real-time validation on text change

#### 7.2.7 RestTimerViewModel

**Responsibilities**:
- Manage rest timer countdown
- Handle pause/resume/skip
- Trigger feedback at completion

**Properties**:
```swift
var duration: Int // total seconds
var remainingSeconds: Int
var isRunning: Bool = false
var isPaused: Bool = false
var progress: Double // 0.0 to 1.0
var timerCancellable: AnyCancellable?
```

**Methods**:
```swift
func start()
func pause()
func resume()
func skip()
func stop()
private func triggerHapticFeedback()
private func playCompletionSound()
```

**Implementation Details**:
- Uses Combine's Timer.publish(every: 1, on: .main)
- Background task continues for 3 minutes max
- Haptic: UIImpactFeedbackGenerator with .medium impact
- Audio: AVFoundation for system sound

#### 7.2.8 HomeViewModel

**Responsibilities**:
- Fetch active plan
- Fetch last workout session
- Check today's check-in status

**Properties**:
```swift
var activePlan: WorkoutPlan?
var lastSession: WorkoutSession?
var todayCheckIn: CheckIn?
var currentDate: Date = Date()
```

**Methods**:
```swift
func loadData(context: ModelContext)
func fetchActivePlan(context: ModelContext) -> WorkoutPlan?
func fetchLastSession(context: ModelContext) -> WorkoutSession?
func fetchTodayCheckIn(context: ModelContext) -> CheckIn?
```

#### 7.2.9 CheckInViewModel

**Responsibilities**:
- Calculate check-in streaks
- Load monthly statistics
- Manage calendar data

**Properties**:
```swift
var currentStreak: Int = 0
var bestStreak: Int = 0
var monthlyCheckIns: [CheckIn] = []
var selectedMonth: Date = Date()
```

**Methods**:
```swift
func calculateStreaks(context: ModelContext)
func loadMonthlyData(for month: Date, context: ModelContext)
func checkInsForDay(_ date: Date) -> [CheckIn]
func monthsWithCheckIns(context: ModelContext) -> [Date]
```

**Streak Algorithm**:
1. Fetch all check-ins ordered by date descending
2. Start from today, count consecutive days with check-ins
3. Missing day breaks current streak
4. Best streak is longest consecutive sequence ever

#### 7.2.10 RegisterCheckInViewModel

**Responsibilities**:
- Manage check-in registration form
- Handle photo selection/capture
- Compress and save images
- Validate inputs

**Properties**:
```swift
var exerciseType: String = "Gym"
var title: String = ""
var calories: String = ""
var location: String = ""
var selectedDate: Date = Date()
var selectedImage: UIImage?
var photoData: Data?
var isShowingCamera: Bool = false
var isShowingPhotoPicker: Bool = false
var errorMessage: String?
```

**Methods**:
```swift
func validate() -> Bool
func compressImage(_ image: UIImage) -> Data?
func saveCheckIn(context: ModelContext) throws
```

**Validation Rules**:
- Exercise type required (from predefined list)
- Title required, max 100 chars
- Calories optional, positive integer if provided
- Location optional, max 200 chars
- Date must not be in future
- Photo optional, compressed to <200KB JPEG

#### 7.2.11 ProgressViewModel

**Responsibilities**:
- Load workout history
- Load exercise statistics
- Group exercises by muscle group
- Calculate personal records

**Properties**:
```swift
enum ProgressTab: String, CaseIterable {
    case workouts = "Treinos"
    case exercises = "Exercícios"
}

var selectedTab: ProgressTab = .workouts
var completedSessions: [WorkoutSession] = []
var executedExercises: [ExerciseStats] = []
var isLoading: Bool = false
```

**Methods**:
```swift
func loadWorkoutHistory(context: ModelContext, limit: Int = 50)
func loadExerciseHistory(context: ModelContext)
func exercisesForMuscleGroup(_ group: MuscleGroup) -> [ExerciseStats]
func personalRecord(for exercise: ExerciseStats) -> ExerciseSet?
```

**Data Structure**:
```swift
struct ExerciseStats {
    let exerciseId: UUID
    let name: String
    let muscleGroup: MuscleGroup
    let lastExecuted: Date
    let totalSets: Int
    let allSets: [ExerciseSet]
}
```

---

## 8. Navigation & Flow

### 8.1 App Structure

```
TabView (ContentView)
├── Tab 1: Home (HomeView)
│   └── Navigation actions to other tabs
├── Tab 2: Treinos (WorkoutsTabView)
│   ├── Segment: Planos (WorkoutPlanListView)
│   │   ├── NavigationStack
│   │   ├── → WorkoutPlanDetailView
│   │   │   ├── Sheet: EditWorkoutPlanView
│   │   │   ├── Sheet: SelectExerciseSourceView
│   │   │   │   ├── → AddExerciseView
│   │   │   │   └── → SelectExistingExerciseView
│   │   │   └── → ExecuteWorkoutView
│   │   │       ├── → ExecuteExerciseView
│   │   │       │   └── Sheet: RestTimerView
│   │   │       └── → WorkoutSummaryView
│   │   └── Sheet: CreateWorkoutPlanView
│   │       └── Sheet: AddExerciseView
│   └── Segment: Biblioteca (ExerciseLibraryView)
│       └── Sheet: AddExerciseToLibraryView
├── Tab 3: Progresso (ProgressView)
│   ├── Segment: Treinos (WorkoutHistoryListView)
│   │   └── → SessionDetailView
│   └── Segment: Exercícios (MuscleGroupListView)
│       └── → MuscleGroupExercisesView
│           └── → ExerciseHistoryView
└── Tab 4: Check-in (CheckInView)
    ├── → RegisterCheckInView
    │   └── Sheet: Camera/PhotoPicker
    └── → ViewAllCheckInsView
```

### 8.2 Navigation Patterns

#### 8.2.1 NavigationStack
- Used for hierarchical navigation (push/pop)
- Each tab has its own NavigationStack
- Back button automatically provided
- Toolbar for actions

#### 8.2.2 Sheet Presentations
- Modal forms (create, edit)
- Full-screen or large detents
- Dismiss with "Cancelar" or after save
- State managed by @State boolean

#### 8.2.3 Tab Switching
- TabView at root level
- Switching tabs returns to root of that tab
- State persists within session

### 8.3 Navigation Flows

#### Flow 1: Create Workout Plan
1. WorkoutPlanListView
2. Tap "+" → Sheet: CreateWorkoutPlanView
3. Tap "Adicionar Exercício" → Sheet: AddExerciseView
4. Save exercise → Returns to CreateWorkoutPlanView
5. Tap "Salvar" → Dismisses sheet, plan appears in list

#### Flow 2: Execute Workout
1. WorkoutPlanDetailView or HomeView
2. Tap "Iniciar Treino" → NavigationLink: ExecuteWorkoutView
3. Tap exercise → NavigationLink: ExecuteExerciseView
4. Complete set → Sheet: RestTimerView (auto-dismisses)
5. Complete all exercises or tap "Finalizar"
6. → NavigationLink: WorkoutSummaryView
7. Tap "Concluir" → Dismiss to root (Home or Detail)

#### Flow 3: Register Check-In
1. HomeView or CheckInView
2. Tap "Fazer Check-in" → NavigationLink: RegisterCheckInView
3. Tap "Add Photo" → Sheet: Camera or PhotoPicker
4. Select photo → Dismiss sheet, photo appears in form
5. Fill form and tap "Check In" → Dismiss to previous view

#### Flow 4: View Progress
1. ProgressView → Treinos tab
2. Tap session → NavigationLink: SessionDetailView
3. Back button returns to list
4. Switch to Exercícios tab
5. Tap muscle group → NavigationLink: MuscleGroupExercisesView
6. Tap exercise → NavigationLink: ExerciseHistoryView

---

## 9. Validation Rules

### 9.1 Workout Plan Validation

| Field | Required | Min Length | Max Length | Type | Additional Rules |
|-------|----------|------------|------------|------|------------------|
| name | Yes | 1 | 100 | String | Cannot be only whitespace |
| desc | No | 0 | 500 | String | Can be empty |
| exercises | No | 0 | Unlimited | Array | Empty plans allowed |

**Error Messages**:
- Empty name: "Nome do plano é obrigatório"
- Name too long: "Nome deve ter no máximo 100 caracteres"

### 9.2 Exercise Validation

| Field | Required | Min | Max | Type | Additional Rules |
|-------|----------|-----|-----|------|------------------|
| name | Yes | 1 | 100 | String | Cannot be only whitespace |
| muscleGroup | Yes | - | - | Enum | Must be valid MuscleGroup case |
| sets | Yes | 1 | 999 | Int | Positive integer |
| reps | Yes | 1 | 999 | Int | Positive integer |
| restSeconds | Yes | 0 | 999 | Int | Non-negative |
| videoURL | No | 0 | 500 | String | Valid URL format if provided |

**Error Messages**:
- Empty name: "Nome do exercício é obrigatório"
- Sets < 1: "Séries devem ser maior ou igual a 1"
- Reps < 1: "Repetições devem ser maior ou igual a 1"
- Invalid URL: "URL do vídeo é inválida"

### 9.3 Exercise Set Validation (During Execution)

| Field | Required | Min | Max | Type | Additional Rules |
|-------|----------|-----|-----|------|------------------|
| weight | No | 0.0 | 9999.9 | Double? | Nil = bodyweight, if provided must be positive |
| reps | Yes | 1 | 999 | Int | Must be positive integer |

**Validation Logic**:
```swift
func validateWeight(_ text: String) -> Bool {
    if text.isEmpty { return true } // bodyweight
    guard let value = Double(text), value > 0 else { return false }
    return true
}

func validateReps(_ text: String) -> Bool {
    guard let value = Int(text), value > 0 else { return false }
    return true
}
```

**Real-time Validation**:
- Validates on every text change
- Shows red border and error message immediately
- Prevents saving until valid

**Error Messages**:
- Invalid weight: "Peso deve ser um número positivo"
- Empty reps: "Repetições são obrigatórias"
- Reps ≤ 0: "Repetições devem ser maior que zero"

### 9.4 Check-In Validation

| Field | Required | Min Length | Max Length | Type | Additional Rules |
|-------|----------|------------|------------|------|------------------|
| exerciseType | Yes | - | - | String | Must be from predefined list |
| title | Yes | 1 | 100 | String | Cannot be only whitespace |
| calories | No | 0 | 99999 | Int? | Positive integer if provided |
| location | No | 0 | 200 | String | Free text |
| date | Yes | - | - | Date | Cannot be future date |
| photoData | No | - | ~200KB | Data? | Compressed JPEG |

**Date Validation**:
```swift
func validateDate(_ date: Date) -> Bool {
    return date <= Date()
}
```

**Photo Compression**:
```swift
func compressImage(_ image: UIImage) -> Data? {
    // Try 0.7 quality first
    if let data = image.jpegData(compressionQuality: 0.7), data.count < 200_000 {
        return data
    }
    // If still too large, try 0.5
    if let data = image.jpegData(compressionQuality: 0.5), data.count < 200_000 {
        return data
    }
    // If still too large, try 0.3
    return image.jpegData(compressionQuality: 0.3)
}
```

**Error Messages**:
- Missing exercise type: "Selecione um tipo de exercício"
- Empty title: "Título é obrigatório"
- Future date: "Data não pode ser no futuro"
- Invalid calories: "Calorias devem ser um número positivo"

### 9.5 Search Validation

**No strict validation**, but behavior:
- Case-insensitive search
- Searches in: plan name, plan description, exercise name
- Empty search shows all results
- No results shows ContentUnavailableView.search

### 9.6 Permission Handling

#### Camera Permission
```swift
import AVFoundation

func requestCameraPermission() {
    AVCaptureDevice.requestAccess(for: .video) { granted in
        if granted {
            // Open camera
        } else {
            // Show error: "Acesso à câmera negado"
        }
    }
}
```

#### Photo Library Permission
```swift
import Photos

func requestPhotoLibraryPermission() {
    PHPhotoLibrary.requestAuthorization { status in
        if status == .authorized {
            // Open photo picker
        } else {
            // Show error: "Acesso à galeria negado"
        }
    }
}
```

**Info.plist Entries Required**:
```xml
<key>NSCameraUsageDescription</key>
<string>Precisamos de acesso à câmera para tirar fotos do seu treino</string>

<key>NSPhotoLibraryUsageDescription</key>
<string>Precisamos de acesso à galeria para selecionar fotos do seu treino</string>
```

---

## 10. User Flows & Scenarios

### 10.1 Complete User Journeys

#### Journey 1: First Time User - Complete Onboarding

**Scenario**: New user opens app for first time and completes first workout.

**Steps**:
1. App launches → ContentView with TabView
2. HomeView shows empty states (no active plan, no last workout)
3. User taps "Treinos" tab
4. WorkoutPlanListView shows EmptyStateView
5. User taps "+" button
6. CreateWorkoutPlanView sheet appears
7. User enters:
   - Name: "Treino de Peito"
   - Description: "Foco em peito e tríceps"
8. User taps "Adicionar Exercício"
9. AddExerciseView sheet appears
10. User enters:
    - Name: "Supino Reto"
    - Muscle Group: Peito
    - Sets: 4
    - Reps: 10
    - Rest: 90 seconds
11. User taps "Salvar" → Returns to CreateWorkoutPlanView
12. User repeats steps 8-11 for 2 more exercises
13. User taps "Salvar" on CreateWorkoutPlanView
14. Plan appears in WorkoutPlanListView
15. User taps the new plan → WorkoutPlanDetailView
16. User taps "Ativar" in toolbar
17. Plan gets "ATIVO" badge
18. User taps "Iniciar Treino"
19. ExecuteWorkoutView appears with 3 exercises
20. User taps first exercise
21. ExecuteExerciseView appears
22. User enters: Weight: 60, Reps: 10
23. User taps "Salvar Série"
24. RestTimerView appears with 90-second countdown
25. Timer counts down, vibrates and beeps at 0
26. User dismisses timer, enters second set
27. User completes all 4 sets for first exercise
28. User returns to exercise list (back button)
29. First exercise shows ✅ badge
30. User completes remaining exercises
31. User taps "Finalizar Treino"
32. WorkoutSummaryView appears:
    - Duration: 45 min
    - Exercises: 3 completados
    - Total sets: 12
    - Total reps: 120
33. User taps "Concluir"
34. Returns to HomeView
35. Home now shows "Último Treino" card
36. Success! First workout complete.

**Expected Duration**: 15-20 minutes

#### Journey 2: Daily Check-In with Photo

**Scenario**: User completes morning workout and registers check-in.

**Steps**:
1. User finishes workout at gym
2. Opens app → HomeView
3. Check-in card shows "Fazer Check-in" button
4. User taps "Fazer Check-in"
5. RegisterCheckInView appears
6. User taps "Add Photo"
7. Action sheet appears: "Open Camera" | "Choose from Gallery"
8. User selects "Open Camera"
9. System requests camera permission (if first time)
10. User grants permission
11. Camera opens
12. User takes selfie
13. Camera dismisses, photo appears in form
14. User fills form:
    - Exercise Type: Gym (selected)
    - Title: "Treino pesado hoje!"
    - Calories: 450
    - Location: "Smart Fit"
    - Date/Time: (defaults to now)
15. User taps "Check In" button
16. Validation passes
17. Photo compressed to JPEG
18. Check-in saved to database
19. Returns to HomeView
20. Home check-in card now shows ✓ "Check-in realizado!"
21. User taps "Check-in" tab
22. CheckInView calendar shows today's date with photo
23. Total count incremented: "17 check-ins"
24. Current streak updated: "🔥 Sequência Atual: 4 dias"
25. Success! Check-in registered.

**Expected Duration**: 2-3 minutes

#### Journey 3: Browse Exercise History and Track Progress

**Scenario**: User wants to see their progress on "Supino Reto" exercise.

**Steps**:
1. User taps "Progresso" tab
2. ProgressView appears with "Treinos" tab selected
3. User sees list of completed workouts
4. User switches to "Exercícios" tab
5. MuscleGroupListView appears with 7 groups
6. User taps "Peito" card
7. MuscleGroupExercisesView appears
8. Shows all chest exercises executed:
   - Supino Reto (último: há 2 dias, 15× executado)
   - Supino Inclinado (último: há 5 dias, 8× executado)
9. User taps "Supino Reto"
10. ExerciseHistoryView appears
11. Shows statistics:
    - Recorde Pessoal: 80kg × 8 reps
    - Última Execução: há 2 dias
    - Total de Séries: 60 séries
12. Scrollable list shows all 60 sets:
    - 20/01/2026: 80kg × 10 | Treino de Peito
    - 20/01/2026: 80kg × 8 | Treino de Peito
    - 20/01/2026: 75kg × 10 | Treino de Peito
    - (continues...)
13. User sees progression from 60kg to 80kg over time
14. User motivated by visible progress!
15. Success! Progress tracked and visualized.

**Expected Duration**: 2-3 minutes

#### Journey 4: Resume Incomplete Workout

**Scenario**: User started a workout but had to leave. Now they resume it.

**Steps**:
1. User previously started "Treino de Pernas"
2. Completed 2 of 5 exercises, then left gym
3. Next day, user opens WorkoutPlanDetailView
4. User taps "Iniciar Treino"
5. Alert appears:
   - "Você tem um treino em andamento"
   - "Última atualização: há 1 dia"
   - [Retomar Treino] [Abandonar e Iniciar Novo]
6. User taps "Retomar Treino"
7. ExecuteWorkoutView appears
8. First 2 exercises show ✅ (complete)
9. Remaining 3 exercises show ⚪ (pending)
10. User taps 3rd exercise
11. ExecuteExerciseView shows previous sets already saved
12. User continues from where they left off
13. User completes remaining exercises
14. User taps "Finalizar Treino"
15. WorkoutSummaryView shows:
    - Duration: calculated from original start (yesterday)
    - All 5 exercises marked complete
16. Success! Workout resumed and completed.

**Alternative Path - Abandon**:
6. User taps "Abandonar e Iniciar Novo"
7. Old session marked complete with partial data
8. New session created
9. All exercises show ⚪ (fresh start)
10. User proceeds with new workout

**Expected Duration**: Variable (depends on workout length)

### 10.2 Edge Cases & Error Scenarios

#### Edge Case 1: No Internet / Offline Usage

**Scenario**: User in gym with no internet connection.

**Expected Behavior**:
- ✅ All features work normally (100% offline app)
- ✅ Data persists locally in SwiftData
- ✅ No sync features currently, so no issues
- ✅ Camera and gallery work offline
- ❌ Video URLs won't load preview (future feature)

#### Edge Case 2: Storage Full / Photo Save Fails

**Scenario**: Device storage full, can't save check-in photo.

**Expected Behavior**:
1. User takes photo for check-in
2. Compression attempt fails (no space)
3. Error alert: "Não foi possível salvar a foto. Verifique o espaço disponível."
4. Check-in form remains open
5. User can proceed without photo or free up space

**Implementation**:
```swift
do {
    try viewModel.saveCheckIn(context: modelContext)
} catch {
    errorMessage = "Erro ao salvar: \(error.localizedDescription)"
    isShowingError = true
}
```

#### Edge Case 3: Very Long Workout Session (Hours)

**Scenario**: User starts workout, leaves app open for 6 hours.

**Expected Behavior**:
- ✅ Session remains active
- ✅ All saved sets persist
- ✅ Duration calculated from startDate
- ⚠️ Background timer expires after 3 minutes (expected)
- ✅ User can still complete workout

**Display**: Duration shows "6h 15m" in summary

#### Edge Case 4: Rapid Tap on Save Button

**Scenario**: User double-taps save button, trying to create duplicate.

**Expected Behavior**:
- ViewModel should have loading state
- Disable button during save operation
- Prevent duplicate entries

**Implementation**:
```swift
@Observable
final class CreateWorkoutPlanViewModel {
    var isSaving: Bool = false
    
    func save(context: ModelContext) throws {
        guard !isSaving else { return }
        isSaving = true
        defer { isSaving = false }
        
        // Save logic...
    }
}

// In View
PrimaryButton(title: "Salvar", isEnabled: !viewModel.isSaving) {
    viewModel.save(context: modelContext)
}
```

#### Edge Case 5: Delete Active Plan with Incomplete Session

**Scenario**: User has active plan with incomplete workout session, then deletes the plan.

**Expected Behavior**:
1. User deletes active plan
2. Plan deleted (cascade deletes exercises)
3. WorkoutSession preserved (relationship is nullify/denormalized)
4. Session's `planId` still valid (UUID snapshot)
5. Session can still be viewed in history
6. No plan is active anymore
7. Home shows "Nenhum plano ativo"

---

## 11. Success Criteria & Testing

### 11.1 Performance Benchmarks

| Operation | Target Time | Metric |
|-----------|-------------|--------|
| App Launch | < 2 seconds | Time to render HomeView |
| Plan List Load | < 1 second | With 50+ plans |
| Start Workout | < 500ms | Create session and navigate |
| Save Set | < 200ms | Persist to database |
| Load History | < 2 seconds | Fetch 100+ sessions |
| Calendar Render | < 1 second | Month with 30 check-ins |
| Photo Compression | < 3 seconds | 12MP image → <200KB |
| Search Filter | < 100ms | Filter 100+ plans |

### 11.2 Data Integrity Tests

#### Test 1: Cascade Delete Verification
```swift
// Given: Plan with 5 exercises
let plan = WorkoutPlan(name: "Test Plan")
plan.exercises = [ex1, ex2, ex3, ex4, ex5]
modelContext.insert(plan)
try modelContext.save()

// When: Delete plan
modelContext.delete(plan)
try modelContext.save()

// Then: All 5 exercises deleted
let descriptor = FetchDescriptor<Exercise>()
let remaining = try modelContext.fetch(descriptor)
XCTAssertEqual(remaining.count, 0)
```

#### Test 2: Only One Active Plan
```swift
// Given: 3 plans, one active
plan1.isActive = true
plan2.isActive = false
plan3.isActive = false

// When: Activate plan2
viewModel.toggleActive(plan: plan2, context: modelContext)

// Then: Only plan2 is active
XCTAssertFalse(plan1.isActive)
XCTAssertTrue(plan2.isActive)
XCTAssertFalse(plan3.isActive)
```

#### Test 3: Incremental Set Persistence
```swift
// Given: Active workout session
let session = WorkoutSession(planId: plan.id, planName: plan.name)

// When: Save 3 sets without finalizing
viewModel.saveSet(set1, context: modelContext)
viewModel.saveSet(set2, context: modelContext)
viewModel.saveSet(set3, context: modelContext)

// Force app termination simulation
// (in real test, would restart app)

// Then: All 3 sets persist
let descriptor = FetchDescriptor<ExerciseSet>(
    predicate: #Predicate { $0.session?.id == session.id }
)
let savedSets = try modelContext.fetch(descriptor)
XCTAssertEqual(savedSets.count, 3)
```

### 11.3 User Experience Tests

#### Test 1: Real-time Validation Feedback
```
Given: User on ExecuteExerciseView
When: User types "0" in reps field
Then: Field border turns red immediately
And: Error message appears: "Repetições devem ser maior que zero"
And: Save button remains disabled

When: User changes to "10"
Then: Border returns to normal
And: Error message disappears
And: Save button becomes enabled
```

#### Test 2: Rest Timer Background Behavior
```
Given: User completed a set
And: Rest timer started (90 seconds)
When: User minimizes app after 30 seconds
And: Waits 60 seconds
Then: Timer continues in background
And: At 0 seconds, haptic feedback triggers
And: Audio notification plays
And: User opens app, timer shows completed

Given: Timer started 5 minutes ago
When: User minimizes app
And: Waits 10 minutes
Then: Timer stopped (3 minute background limit)
And: User opens app, timer shows "expired" state
```

#### Test 3: Image Compression Quality
```
Given: User selects 12MP photo (4000×3000 pixels, 8MB)
When: RegisterCheckInViewModel processes image
Then: Compressed to JPEG <200KB
And: Visual quality remains acceptable
And: Check-in saves successfully
And: Calendar displays photo without distortion
```

### 11.4 Edge Case Tests

#### Test 1: Empty Plan Execution
```
Given: Workout plan with 0 exercises
When: User taps "Iniciar Treino"
Then: ExecuteWorkoutView shows empty state
And: User can immediately "Finalizar Treino"
And: Summary shows 0 exercises, 0 sets
```

#### Test 2: Very Large Numbers
```
Given: User enters set data
When: Weight = 9999.9, Reps = 999
Then: Validation passes
And: Set saves successfully
And: Displays correctly with locale formatting
```

#### Test 3: Future Date Prevention
```
Given: User on RegisterCheckInView
When: User opens date picker
Then: Future dates are disabled/not selectable
And: Selecting today or past dates allowed
```

### 11.5 Accessibility Checks

| Feature | VoiceOver Label | Expected |
|---------|-----------------|----------|
| Plan Row | "Treino de Peito, 5 exercícios, ativo" | Clear context |
| Exercise Row | "Supino Reto, Peito, 4 séries, 10 repetições" | Full details |
| Save Button | "Salvar plano" | Action clear |
| Active Badge | "Plano ativo" | Status clear |
| Progress | "3 de 8 exercícios completos" | Numeric progress |

### 11.6 Localization Tests (Portuguese)

| Value | Input | Display | Correct |
|-------|-------|---------|---------|
| Decimal | 80.5 | "80,5 kg" | ✅ |
| Large Number | 1000 | "1.000" | ✅ |
| Date | 2026-01-20 | "20/01/2026" | ✅ |
| Relative Time | 2 days ago | "Há 2 dias" | ✅ |
| Duration | 3665 seconds | "1h 1m" | ✅ |

---

## 12. Future Enhancements

### 12.1 Planned Features (Not Yet Implemented)

#### 12.1.1 Cloud Sync
- Sync workout plans across devices (iCloud or custom backend)
- Conflict resolution strategies
- Offline-first with background sync

#### 12.1.2 Exercise Video Tutorials
- Video playback integration for `videoURL` field
- Embedded YouTube player or native video player
- Picture-in-picture during workout execution

#### 12.1.3 Workout Templates
- Pre-built workout plans from fitness experts
- Template marketplace or library
- Clone and customize templates

#### 12.1.4 Advanced Analytics
- Charts and graphs (weight progression over time)
- Volume tracking (sets × reps × weight)
- Muscle group balance analysis
- Rest days vs workout days ratio

#### 12.1.5 Social Features
- Share workouts with friends
- Leaderboards and challenges
- Community check-in feed
- Follow other users

#### 12.1.6 Nutrition Tracking
- Meal logging
- Macro/calorie targets
- Integration with check-ins
- Photos of meals

#### 12.1.7 Wearable Integration
- Apple Watch companion app
- Real-time heart rate monitoring during workouts
- Workout controls on watch
- Haptic timer feedback on wrist

#### 12.1.8 Advanced Rest Timer
- Configurable timer sounds
- Gradual countdown warnings (30s, 10s, 5s)
- Custom rest times per set (different for each set)
- Auto-adjust rest based on RPE (Rate of Perceived Exertion)

#### 12.1.9 Workout Notes
- Per-set notes ("felt heavy", "easy")
- Per-workout notes (summary, mood)
- Voice notes during workout
- Photo notes (equipment settings)

#### 12.1.10 Export Data
- Export workout history to CSV
- PDF reports
- Integration with Apple Health
- Backup and restore functionality

### 12.2 Architectural Improvements

#### 12.2.1 Unit Testing
- Full test coverage for ViewModels
- Mock ModelContext for testing
- UI testing with XCTest
- Snapshot testing for views

#### 12.2.2 Dependency Injection
- Protocol-based repositories
- Testable architecture
- Swap implementations (e.g., mock database for tests)

#### 12.2.3 Error Handling
- Centralized error handling
- User-friendly error messages
- Retry mechanisms
- Logging and crash reporting

#### 12.2.4 Localization
- Multi-language support (English, Spanish, etc.)
- Locale-aware formatting
- RTL language support
- Localized content

### 12.3 Extensibility Points

**Current architecture supports**:

1. **Adding New Exercise Types**: Extend `ExerciseType` enum
2. **Adding Muscle Groups**: Extend `MuscleGroup` enum with colors and icons
3. **Custom Metrics**: Add fields to `ExerciseSet` for RPE, tempo, etc.
4. **Additional Plan Types**: Add workout program types (strength, hypertrophy, endurance)
5. **Timer Variations**: Subclass or extend `RestTimerViewModel` for different timer behaviors

---

## Appendix A: Code Snippets

### A.1 SwiftData ModelContainer Setup

```swift
import SwiftUI
import SwiftData

@main
struct NaNucaApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
        .modelContainer(for: [
            WorkoutPlan.self,
            Exercise.self,
            WorkoutSession.self,
            ExerciseSet.self,
            CheckIn.self
        ])
    }
}
```

### A.2 Querying Data with @Query

```swift
import SwiftUI
import SwiftData

struct WorkoutPlanListView: View {
    @Query(
        sort: \WorkoutPlan.modifiedDate,
        order: .reverse
    ) private var plans: [WorkoutPlan]
    
    var body: some View {
        List {
            ForEach(plans) { plan in
                WorkoutPlanRowView(plan: plan)
            }
        }
    }
}
```

### A.3 Complex FetchDescriptor Example

```swift
func loadWorkoutHistory(context: ModelContext) {
    var descriptor = FetchDescriptor<WorkoutSession>(
        predicate: #Predicate { session in
            session.isCompleted == true
        },
        sortBy: [
            SortDescriptor(\WorkoutSession.startDate, order: .reverse)
        ]
    )
    descriptor.fetchLimit = 50
    descriptor.relationshipKeyPathsForPrefetching = [
        \WorkoutSession.exerciseSets
    ]
    
    completedSessions = (try? context.fetch(descriptor)) ?? []
}
```

### A.4 Rest Timer with Combine

```swift
import Combine
import SwiftUI
import AVFoundation

@Observable
final class RestTimerViewModel {
    var remainingSeconds: Int
    var isRunning: Bool = false
    private var timerCancellable: AnyCancellable?
    
    init(duration: Int) {
        self.remainingSeconds = duration
    }
    
    func start() {
        isRunning = true
        timerCancellable = Timer.publish(every: 1, on: .main, in: .common)
            .autoconnect()
            .sink { [weak self] _ in
                guard let self = self else { return }
                if self.remainingSeconds > 0 {
                    self.remainingSeconds -= 1
                } else {
                    self.complete()
                }
            }
    }
    
    func complete() {
        isRunning = false
        timerCancellable?.cancel()
        triggerHapticFeedback()
        playCompletionSound()
    }
    
    private func triggerHapticFeedback() {
        let generator = UIImpactFeedbackGenerator(style: .medium)
        generator.impactOccurred()
    }
    
    private func playCompletionSound() {
        AudioServicesPlaySystemSound(1057) // System sound
    }
}
```

### A.5 Image Compression Utility

```swift
import UIKit

extension UIImage {
    func compressToJPEG(targetSizeKB: Int = 200) -> Data? {
        let targetBytes = targetSizeKB * 1024
        
        // Try compression levels
        let compressionLevels: [CGFloat] = [0.7, 0.5, 0.3, 0.1]
        
        for quality in compressionLevels {
            guard let data = self.jpegData(compressionQuality: quality) else {
                continue
            }
            if data.count <= targetBytes {
                return data
            }
        }
        
        // If still too large, resize image
        let scale: CGFloat = sqrt(CGFloat(targetBytes) / CGFloat(self.jpegData(compressionQuality: 0.1)?.count ?? 1))
        let newSize = CGSize(
            width: self.size.width * scale,
            height: self.size.height * scale
        )
        
        UIGraphicsBeginImageContextWithOptions(newSize, false, 1.0)
        self.draw(in: CGRect(origin: .zero, size: newSize))
        let resized = UIGraphicsGetImageFromCurrentImageContext()
        UIGraphicsEndImageContext()
        
        return resized?.jpegData(compressionQuality: 0.5)
    }
}
```

---

## Appendix B: Glossary

| Term | Definition |
|------|------------|
| **MVVM** | Model-View-ViewModel architectural pattern |
| **SwiftData** | Apple's modern data persistence framework (iOS 17+) |
| **@Model** | Macro that makes a class persistable with SwiftData |
| **@Query** | Property wrapper that automatically fetches and observes SwiftData objects |
| **@Observable** | Macro that makes a class observable for UI updates (iOS 17+) |
| **FetchDescriptor** | Type-safe query builder for SwiftData |
| **Predicate** | Type-safe filter condition using #Predicate macro |
| **ModelContext** | SwiftData context for CRUD operations |
| **Cascade Delete** | Automatically delete related objects when parent is deleted |
| **Nullify** | Set relationship to nil when related object is deleted |
| **SF Symbol** | Apple's icon system (system-provided icons) |
| **Haptic Feedback** | Vibration feedback on user interactions |
| **Sheet** | Modal presentation in SwiftUI |
| **NavigationStack** | SwiftUI's navigation container (iOS 16+) |
| **ViewBuilder** | Function builder for constructing views |
| **Combine** | Apple's reactive programming framework |
| **Publisher** | Combine's event stream |
| **AnyCancellable** | Token for managing Combine subscriptions |
| **PhotosUI** | Framework for photo picking |
| **AVFoundation** | Framework for audio/video playback |
| **ContentUnavailableView** | SwiftUI's empty state component (iOS 17+) |
| **Locale** | System settings for language, region, number formatting |
| **Denormalization** | Storing snapshot copies of data for historical accuracy |
| **Check-in Streak** | Consecutive days with check-ins |
| **Personal Record (PR)** | Highest weight achieved for an exercise |
| **Bodyweight Exercise** | Exercise without external weight (weight field = nil) |
| **Rest Timer** | Countdown timer between sets |
| **Background Task** | Work that continues when app is minimized |
| **Incremental Save** | Saving data progressively, not just at end |

---

## Document Change Log

| Date | Version | Changes | Author |
|------|---------|---------|--------|
| 2026-01-21 | 1.0 | Initial comprehensive documentation | AI Assistant |

---

**End of Documentation**

This documentation provides a complete blueprint for recreating the NaNuca iOS application. Follow the specifications, data models, and architectural patterns described to build a feature-complete fitness tracking app using Swift, SwiftUI, and SwiftData.

For questions or clarifications, refer to the original spec files in the `/specs` directory or the implementation status document.
