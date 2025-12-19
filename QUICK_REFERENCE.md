# MBS Turnier Manager - Quick Reference

## 📋 Projekt-Übersicht

**MBS Turnier Manager** - Single Page Application für Pool-Billard-Turniere

```
┌─────────────────────────────────────────────────────────────┐
│                    MBS Turnier Manager                       │
│                   Single-File HTML SPA                       │
├─────────────────────────────────────────────────────────────┤
│  Admin Manager  │  Scoreboards  │  OBS Overlays            │
└─────────────────────────────────────────────────────────────┘
```

## 🛠️ Tech Stack

```
Frontend:
├── Vanilla JavaScript (ES6+)
├── HTML5
└── Tailwind CSS (Glass/Neon Design)

Backend:
├── Firebase 11.6.1
│   ├── Authentication
│   ├── Firestore
│   └── Real-time Database
│
└── Google Gemini API

Libraries:
├── FontAwesome (Icons)
└── Confetti.js (Effects)
```

## 🎨 Design System

```css
/* Colors */
Background: #050505 (Dark)
Accents:
  ├── Green:      #10b981 (Success, Active)
  ├── Blue:       #3b82f6 (Primary)
  ├── Purple:     #8b5cf6 (Highlights)
  └── Red:        #ef4444 (Errors, Warnings)

/* Glass Effect */
.glass-panel {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}
```

## 🏗️ Architecture

```
index.html
│
├── HTML Structure
│   └── <div id="app"></div>
│
├── CSS
│   ├── Tailwind (CDN)
│   ├── FontAwesome
│   └── Custom Glass/Neon Styles
│
└── JavaScript (Namespaces)
    ├── app         (Core: init, state, routing, auth)
    ├── ui          (Views, components, modals, forms)
    ├── logic       (Business logic, calculations)
    ├── firebase    (Database, auth, real-time)
    ├── gemini      (AI features)
    ├── utils       (Helpers, validators)
    └── obs         (OBS overlays)
```

## 📊 Data Flow

```
User Action
    ↓
Event Handler (ui.*)
    ↓
Business Logic (logic.*)
    ↓
Firebase Operation (firebase.db.*)
    ↓
onSnapshot() Trigger
    ↓
State Update (app.state.set)
    ↓
UI Re-render (ui.render)
    ↓
DOM Update
```

## 🔄 State Management

```javascript
app.state.current = {
  user: null,              // Current user
  isAdmin: false,          // Admin flag
  currentRoute: '/',       // Current route
  tournaments: [],         // Active tournaments
  matches: [],             // Current matches
  players: [],             // Player roster
  ui: {                    // UI state
    loading: false,
    modalOpen: false,
    toasts: []
  },
  settings: {}             // App settings
}
```

## 📁 Firestore Structure

```
/tournaments/{tournamentId}
  ├── name, date, type, status
  ├── players[], matches[]
  ├── /matches/{matchId}
  │   └── player1Id, player2Id, score, status
  └── /enrollments/{playerId}
      └── enrolledAt, status

/players/{playerId}
  ├── name, email, avatar
  └── /stats
      └── matchesPlayed, matchesWon, ranking

/users/{userId}
  └── email, role, displayName

/settings/app
  └── features, config
```

## 🎯 Core Functions (120+ total)

### App Namespace (15+ functions)
```javascript
app.init()                    // Initialize app
app.state.get(key)           // Get state
app.state.set(key, value)    // Update state
app.state.subscribe()        // Subscribe to changes
app.router.navigate(path)    // Navigate routes
app.auth.login()             // User login
app.auth.logout()            // User logout
```

### UI Namespace (40+ functions)
```javascript
// Views
ui.views.dashboard()         // Main dashboard
ui.views.tournamentList()    // Tournament list
ui.views.tournamentDetail()  // Tournament detail
ui.views.scoreboard()        // Scoreboard view
ui.views.adminPanel()        // Admin panel
ui.views.obsOverlay()        // OBS overlay

// Components
ui.components.header()       // Header
ui.components.tournamentCard() // Tournament card
ui.components.matchCard()    // Match card
ui.components.bracketView()  // Bracket visualization

// Modals & Forms
ui.modal.open()              // Open modal
ui.modal.confirm()           // Confirm dialog
ui.forms.createTournament()  // Tournament form
ui.toast.show()              // Toast notification
ui.confetti.celebrate()      // Confetti effect
```

### Logic Namespace (30+ functions)
```javascript
// Tournament
logic.tournament.create()    // Create tournament
logic.tournament.start()     // Start tournament
logic.tournament.complete()  // Complete tournament

// Match
logic.match.create()         // Create match
logic.match.updateScore()    // Update score
logic.match.complete()       // Complete match

// Player
logic.player.create()        // Create player
logic.player.getStats()      // Get statistics
logic.player.enroll()        // Enroll in tournament

// Bracket
logic.bracket.generate()     // Generate bracket
logic.bracket.update()       // Update bracket

// Scoring
logic.scoring.calculate()    // Calculate score
logic.scoring.getRankings()  // Get rankings
```

### Firebase Integration (15+ functions)
```javascript
firebase.db.collection()     // Get collection
firebase.db.get()            // Get document
firebase.db.set()            // Set document
firebase.db.update()         // Update document
firebase.db.query()          // Query collection
firebase.listeners.onSnapshot() // Real-time listener
firebase.auth.signIn()       // Sign in
firebase.auth.signOut()      // Sign out
```

### Gemini AI (5+ functions)
```javascript
gemini.init()                // Initialize API
gemini.generateMatchCommentary() // Match commentary
gemini.analyzeTournament()   // Tournament analysis
gemini.predictOutcome()      // Predict outcome
gemini.generatePlayerProfile() // Player profile
```

### OBS Overlays (10+ functions)
```javascript
obs.init(mode)               // Initialize overlay
obs.scoreboard.show()        // Show scoreboard
obs.scoreboard.update()      // Update scoreboard
obs.bracket.show()           // Show bracket
obs.playerInfo.show()        // Show player info
obs.transition()             // Transition effect
```

## 📱 Views & Routes

```
Route                    View                Handler
─────────────────────────────────────────────────────────
/                        Dashboard           ui.views.dashboard()
/tournaments             Tournament List     ui.views.tournamentList()
/tournament/:id          Tournament Detail   ui.views.tournamentDetail()
/match/:id              Match View          ui.views.matchView()
/scoreboard/:id         Scoreboard          ui.views.scoreboard()
/admin                  Admin Panel         ui.views.adminPanel()
/obs/:mode              OBS Overlay         ui.views.obsOverlay()
```

## 🎮 Features

### ✅ Tournament Management
- Create, edit, delete tournaments
- Player enrollment
- Bracket generation (Single/Double elimination, Round-robin)
- Start/complete tournaments

### ✅ Match Management
- Create matches
- Update scores in real-time
- Complete matches
- Match history

### ✅ Player Management
- Player profiles
- Statistics tracking
- Rankings & leaderboards
- Performance history

### ✅ Admin Panel
- User management
- Tournament administration
- System settings
- Monitoring

### ✅ Scoreboards
- Live match scores
- Tournament brackets
- Real-time updates
- Public display mode

### ✅ OBS Overlays
- Scoreboard overlay
- Match info overlay
- Bracket overlay
- Player info overlay
- Custom transitions

### ✅ AI Features (Gemini)
- Match commentary generation
- Tournament analysis
- Outcome predictions
- Player profile descriptions

## 🔐 Security

```javascript
// Firebase Rules
- Authenticated users: Read access
- Admin only: Write access (tournaments, settings)
- Users: Own profile updates only

// Input Validation
- All inputs validated
- XSS protection (HTML escaping)
- Score validation (game rules)
- Permission checks
```

## 🚀 Performance

```javascript
// Optimizations
- Debouncing: Input handlers
- Throttling: Scroll/resize handlers
- Lazy Loading: Components on demand
- Caching: Frequently accessed data
- Real-time: Selective onSnapshot listeners
- Bundle: Single file (<500KB target)
```

## 📚 Documentation Files

```
README.md           - Project introduction
CODE_ANALYSIS.md    - Complete function index (120+ functions)
ARCHITECTURE.md     - Detailed architecture (German)
UNDERSTANDING.md    - Confirmation of understanding
QUICK_REFERENCE.md  - This file (Quick reference)
```

## 🎯 Development Status

```
Phase 1: Analysis & Documentation
├── [✓] Code analysis completed
├── [✓] Function index created
├── [✓] Architecture documented
├── [✓] Data models defined
└── [✓] Understanding confirmed

Phase 2: Implementation (Next)
├── [ ] Basic HTML structure
├── [ ] Firebase setup
├── [ ] Core features (CRUD)
├── [ ] UI with Glass/Neon design
└── [ ] Real-time updates

Phase 3: Advanced Features
├── [ ] OBS overlays
├── [ ] Admin panel
├── [ ] Statistics
└── [ ] AI integration
```

## 📞 Key Concepts

### Single-File Architecture
✅ Everything in one HTML file  
✅ No build tools required  
✅ Easy deployment  
✅ Self-contained  

### Namespace Organization
✅ Clear separation of concerns  
✅ Modular structure  
✅ Easy to maintain  
✅ Scalable architecture  

### Real-time Sync
✅ Firebase onSnapshot  
✅ Live updates  
✅ Central state  
✅ Unidirectional data flow  

### Glass/Neon Design
✅ Dark theme (#050505)  
✅ Glassmorphism effects  
✅ Neon accent colors  
✅ Modern, sleek UI  

---

## ✅ Status: READY FOR IMPLEMENTATION

**Analysis Complete**: ✓  
**Functions Indexed**: ✓ (120+)  
**Architecture Defined**: ✓  
**Documentation Created**: ✓  

🚀 **Next Step**: Begin Phase 2 Implementation
