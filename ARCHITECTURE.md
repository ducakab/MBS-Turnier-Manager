# MBS Turnier Manager - Architektur Dokumentation

## Projektübersicht

**MBS Turnier Manager** ist eine Single-Page-Application (SPA) zur Verwaltung von Pool-Billard-Turnieren. Die gesamte Anwendung ist in einer einzigen HTML-Datei implementiert.

## Technologie-Stack

### Frontend
- **Vanilla JavaScript** (ES6+)
  - Keine Frameworks
  - Native Browser-APIs
  - Moderne JavaScript-Features
- **HTML5**
  - Semantische Markup
  - Accessibility-freundlich
- **Tailwind CSS**
  - Utility-first CSS
  - Glass/Neon Design-System
  - Responsive Design

### Backend & Services
- **Firebase 11.6.1**
  - Authentication
  - Firestore (NoSQL Database)
  - Real-time Database
  - Cloud Functions (optional)
- **Google Gemini API**
  - AI-gestützte Features
  - Match-Kommentare
  - Turnier-Analysen

### UI Libraries & Effekte
- **FontAwesome** - Icons
- **Confetti.js** - Feier-Effekte
- **Custom Animations** - CSS/JS Transitions

## Design-System

### Farbpalette

#### Primärfarben
```css
/* Hintergrund */
--bg-primary: #050505;      /* Sehr dunkel */
--bg-secondary: #0a0a0a;    /* Dunkel */
--bg-tertiary: #121212;     /* Mittel dunkel */

/* Akzentfarben */
--accent-green: #10b981;    /* Erfolg, Aktiv */
--accent-blue: #3b82f6;     /* Primär */
--accent-purple: #8b5cf6;   /* Highlight */
--accent-red: #ef4444;      /* Fehler, Warnung */

/* Glasmorphismus */
--glass-bg: rgba(255, 255, 255, 0.05);
--glass-border: rgba(255, 255, 255, 0.1);
--glass-shadow: rgba(0, 0, 0, 0.5);
```

#### Farbverwendung
- **Grün**: Erfolgs-Zustände, aktive Elemente, Gewinner
- **Blau-Lila**: Primäre Aktionen, Highlights, Navigation
- **Rot**: Fehler, Löschungen, kritische Warnungen
- **Weiß/Grau**: Text, sekundäre Elemente

### Komponenten-Stile

#### Glass Panel
```css
.glass-panel {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.5);
}
```

#### Buttons
```css
.btn {
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-primary {
  background: linear-gradient(135deg, #3b82f6, #8b5cf6);
}

.btn-success {
  background: linear-gradient(135deg, #10b981, #059669);
}

.btn-danger {
  background: linear-gradient(135deg, #ef4444, #dc2626);
}
```

### Responsive Breakpoints
```css
/* Tablet */
@media (min-width: 768px) { }

/* Desktop */
@media (min-width: 1024px) { }

/* Large Desktop */
@media (min-width: 1280px) { }
```

## Architektur

### Single-File-Struktur

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <!-- Meta Tags -->
  <!-- External CSS (Tailwind CDN) -->
  <!-- FontAwesome -->
  <!-- Custom Styles -->
</head>
<body>
  <!-- App Container -->
  <div id="app"></div>
  
  <!-- External Scripts -->
  <!-- Firebase SDK -->
  <!-- Confetti.js -->
  
  <!-- Application Code -->
  <script>
    // Namespace Definitions
    const app = {};
    const ui = {};
    const logic = {};
    const firebase = {};
    const gemini = {};
    const utils = {};
    const obs = {};
    
    // Implementation
    // ...
    
    // Application Start
    app.init();
  </script>
</body>
</html>
```

### Namespace-Organisation

#### 1. App Namespace (`app`)
**Verantwortlichkeiten:**
- Anwendungs-Initialisierung
- Konfigurations-Management
- State-Management
- Routing
- Authentifizierung
- Lifecycle-Management

**Struktur:**
```javascript
const app = {
  // Konfiguration
  config: {},
  
  // Zentraler State
  state: {
    current: {},
    listeners: [],
    init() {},
    get() {},
    set() {},
    subscribe() {}
  },
  
  // Router
  router: {
    routes: {},
    init() {},
    navigate() {},
    register() {}
  },
  
  // Authentifizierung
  auth: {
    currentUser: null,
    init() {},
    login() {},
    logout() {},
    checkAdmin() {}
  },
  
  // Lifecycle
  init() {},
  ready() {},
  cleanup() {}
};
```

#### 2. UI Namespace (`ui`)
**Verantwortlichkeiten:**
- View-Rendering
- Komponenten-Erstellung
- DOM-Manipulation
- Event-Handling
- Modals & Dialoge
- Formulare
- Loading & Feedback

**Struktur:**
```javascript
const ui = {
  // Core Rendering
  render() {},
  update() {},
  clear() {},
  
  // Views
  views: {
    dashboard() {},
    tournamentList() {},
    tournamentDetail() {},
    matchView() {},
    scoreboard() {},
    adminPanel() {},
    obsOverlay() {}
  },
  
  // Komponenten
  components: {
    header() {},
    navigation() {},
    tournamentCard() {},
    matchCard() {},
    playerCard() {},
    scoreDisplay() {},
    bracketView() {}
  },
  
  // Modals
  modal: {
    open() {},
    close() {},
    confirm() {},
    alert() {}
  },
  
  // Formulare
  forms: {
    createTournament() {},
    editTournament() {},
    addPlayer() {},
    matchScore() {},
    validate() {}
  },
  
  // Feedback
  loading: {
    show() {},
    hide() {}
  },
  toast: {
    show() {}
  },
  confetti: {
    celebrate() {}
  }
};
```

#### 3. Logic Namespace (`logic`)
**Verantwortlichkeiten:**
- Business-Logik
- Daten-Operationen
- Validierung
- Berechnungen
- Turnierregeln
- Score-Berechnung

**Struktur:**
```javascript
const logic = {
  // Turnier-Logik
  tournament: {
    create() {},
    update() {},
    delete() {},
    get() {},
    list() {},
    start() {},
    complete() {}
  },
  
  // Match-Logik
  match: {
    create() {},
    updateScore() {},
    complete() {},
    get() {},
    listByTournament() {}
  },
  
  // Spieler-Logik
  player: {
    create() {},
    update() {},
    get() {},
    list() {},
    getStats() {},
    enroll() {}
  },
  
  // Bracket-Logik
  bracket: {
    generate() {},
    update() {},
    get() {}
  },
  
  // Scoring
  scoring: {
    calculate() {},
    validateScore() {},
    getRankings() {}
  },
  
  // Statistiken
  stats: {
    calculatePlayerStats() {},
    getTournamentStats() {},
    getLeaderboard() {}
  }
};
```

### State-Management

#### Zentraler State
```javascript
app.state.current = {
  // Authentifizierung
  user: null,
  isAdmin: false,
  
  // Navigation
  currentRoute: '/',
  
  // Daten
  tournaments: [],
  matches: [],
  players: [],
  
  // UI-State
  ui: {
    loading: false,
    modalOpen: false,
    activeModal: null,
    toasts: []
  },
  
  // Einstellungen
  settings: {
    theme: 'dark',
    language: 'de',
    notifications: true
  }
};
```

#### State-Flow
```
User Action
  ↓
Event Handler
  ↓
Logic Function
  ↓
Firebase Operation
  ↓
onSnapshot Trigger
  ↓
State Update (app.state.set)
  ↓
State Listeners Notified
  ↓
UI Update (ui.render)
  ↓
DOM Update
```

### Routing-System

#### Hash-basiertes Routing
```javascript
// Route-Definitionen
app.router.routes = {
  '/': 'dashboard',
  '/tournaments': 'tournamentList',
  '/tournament/:id': 'tournamentDetail',
  '/match/:id': 'matchView',
  '/scoreboard/:id': 'scoreboard',
  '/admin': 'adminPanel',
  '/obs/:mode': 'obsOverlay'
};

// Route-Handler
window.addEventListener('hashchange', () => {
  const hash = location.hash.slice(1) || '/';
  app.router.navigate(hash);
});
```

### Firebase-Integration

#### Firestore-Struktur
```
/tournaments/{tournamentId}
  - name: string
  - date: timestamp
  - type: string
  - status: string
  - players: array
  - settings: object
  
  /matches/{matchId}
    - player1Id: string
    - player2Id: string
    - score: object
    - status: string
    - winnerId: string
  
  /enrollments/{playerId}
    - enrolledAt: timestamp
    - status: string

/players/{playerId}
  - name: string
  - email: string
  - avatar: string
  /stats
    - matchesPlayed: number
    - matchesWon: number
    - ranking: number

/users/{userId}
  - email: string
  - role: string
  - displayName: string

/settings/app
  - features: object
  - config: object
```

#### Real-time Listeners
```javascript
// Turnier-Listener
const unsubscribe = firebase.db
  .collection('tournaments')
  .onSnapshot((snapshot) => {
    snapshot.docChanges().forEach((change) => {
      if (change.type === 'added') {
        app.state.set('tournaments', [...tournaments, change.doc.data()]);
      }
      if (change.type === 'modified') {
        // Update tournament in state
      }
      if (change.type === 'removed') {
        // Remove tournament from state
      }
    });
  });
```

### Event-System

#### Custom Events
```javascript
// Event-Dispatcher
const emit = (eventName, detail) => {
  window.dispatchEvent(new CustomEvent(eventName, { detail }));
};

// Event-Listener
window.addEventListener('tournament:created', (e) => {
  console.log('Tournament created:', e.detail);
  ui.toast.show('Turnier erstellt!', 'success');
});

// Event-Liste
const events = {
  // App Events
  'app:init': 'Application initialized',
  'app:ready': 'Application ready',
  
  // Auth Events
  'auth:login': 'User logged in',
  'auth:logout': 'User logged out',
  
  // Tournament Events
  'tournament:created': 'Tournament created',
  'tournament:updated': 'Tournament updated',
  'tournament:started': 'Tournament started',
  'tournament:completed': 'Tournament completed',
  
  // Match Events
  'match:created': 'Match created',
  'match:started': 'Match started',
  'match:score-updated': 'Score updated',
  'match:completed': 'Match completed'
};
```

## Datenmodelle

### Tournament Model
```javascript
{
  id: 'uuid',
  name: 'MBS Cup 2024',
  date: '2024-03-15T18:00:00Z',
  type: 'single-elimination', // 'double-elimination', 'round-robin'
  status: 'upcoming', // 'in-progress', 'completed'
  players: ['player1-id', 'player2-id'],
  matches: ['match1-id', 'match2-id'],
  bracket: {
    rounds: [],
    structure: {}
  },
  settings: {
    maxPlayers: 16,
    gameType: '8-ball',
    raceTo: 5
  },
  createdBy: 'user-id',
  createdAt: '2024-03-01T10:00:00Z',
  updatedAt: '2024-03-01T10:00:00Z'
}
```

### Match Model
```javascript
{
  id: 'uuid',
  tournamentId: 'tournament-id',
  player1Id: 'player1-id',
  player2Id: 'player2-id',
  score: {
    player1: 3,
    player2: 5
  },
  status: 'completed', // 'scheduled', 'in-progress'
  winnerId: 'player2-id',
  round: 1,
  bracketPosition: 'winners-r1-m1',
  startTime: '2024-03-15T18:00:00Z',
  endTime: '2024-03-15T18:45:00Z',
  createdAt: '2024-03-15T17:00:00Z',
  updatedAt: '2024-03-15T18:45:00Z'
}
```

### Player Model
```javascript
{
  id: 'uuid',
  name: 'Max Mustermann',
  email: 'max@example.com',
  avatar: 'https://example.com/avatar.jpg',
  stats: {
    matchesPlayed: 45,
    matchesWon: 28,
    matchesLost: 17,
    tournamentsPlayed: 12,
    tournamentsWon: 3,
    ranking: 1250
  },
  createdAt: '2024-01-01T10:00:00Z',
  updatedAt: '2024-03-15T18:45:00Z'
}
```

## Feature-Module

### 1. Tournament Management
**Features:**
- Turnier erstellen/bearbeiten/löschen
- Spieler-Einschreibung
- Bracket-Generierung
- Turnier starten/beenden
- Turnier-Einstellungen

**UI-Komponenten:**
- Tournament List
- Tournament Card
- Tournament Detail
- Tournament Form
- Tournament Settings

### 2. Match Management
**Features:**
- Match erstellen
- Score eingeben/aktualisieren
- Match abschließen
- Match-Historie
- Live-Updates

**UI-Komponenten:**
- Match Card
- Match Detail
- Score Input
- Match Status

### 3. Player Management
**Features:**
- Spieler-Profile
- Statistiken
- Rangliste
- Spieler-Historie

**UI-Komponenten:**
- Player Card
- Player Profile
- Stats Display
- Leaderboard

### 4. Admin Panel
**Features:**
- Nutzer-Verwaltung
- Turnier-Verwaltung
- Einstellungen
- System-Monitoring

**UI-Komponenten:**
- Admin Dashboard
- User Management
- Settings Panel

### 5. Scoreboard
**Features:**
- Live-Scores
- Bracket-Ansicht
- Match-Status
- Aktualisierungen in Echtzeit

**UI-Komponenten:**
- Scoreboard Display
- Bracket Visualization
- Live Score Updates

### 6. OBS Overlays
**Features:**
- Scoreboard-Overlay
- Match-Info-Overlay
- Bracket-Overlay
- Player-Info-Overlay
- Custom-Transitions

**UI-Komponenten:**
- Overlay Container
- Score Display
- Player Names
- Match Info
- Transition Effects

## Performance-Optimierung

### Lade-Performance
1. **Critical CSS**: Inline kritisches CSS
2. **Lazy Loading**: Komponenten bei Bedarf laden
3. **Code Splitting**: Logische Trennung der Namespaces
4. **Asset Optimization**: Minimierte Assets

### Runtime-Performance
1. **Debouncing**: Input-Handler debounced
2. **Throttling**: Scroll-/Resize-Handler throttled
3. **Virtual Scrolling**: Bei langen Listen
4. **Memoization**: Berechnungen cachen

### Firebase-Optimierung
1. **Selective Listening**: Nur benötigte Daten subscriben
2. **Query Optimization**: Effiziente Queries
3. **Offline Persistence**: Firebase offline cache
4. **Batch Operations**: Mehrere Operationen batchen

## Sicherheit

### Firebase Security Rules
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Tournaments
    match /tournaments/{tournamentId} {
      allow read: if request.auth != null;
      allow create, update, delete: if request.auth != null 
        && get(/databases/$(database)/documents/users/$(request.auth.uid)).data.role == 'admin';
      
      // Matches
      match /matches/{matchId} {
        allow read: if request.auth != null;
        allow write: if request.auth != null 
          && get(/databases/$(database)/documents/users/$(request.auth.uid)).data.role == 'admin';
      }
    }
    
    // Players
    match /players/{playerId} {
      allow read: if request.auth != null;
      allow update: if request.auth != null 
        && request.auth.uid == playerId;
      allow create, delete: if request.auth != null 
        && get(/databases/$(database)/documents/users/$(request.auth.uid)).data.role == 'admin';
    }
    
    // Users
    match /users/{userId} {
      allow read: if request.auth != null;
      allow write: if request.auth != null 
        && request.auth.uid == userId;
    }
  }
}
```

### Input-Validierung
```javascript
// Alle Inputs validieren
const validateTournamentData = (data) => {
  if (!data.name || data.name.length < 3) {
    throw new Error('Turniername muss mindestens 3 Zeichen haben');
  }
  if (!data.date || new Date(data.date) < new Date()) {
    throw new Error('Turnierdatum muss in der Zukunft liegen');
  }
  // Weitere Validierungen...
  return true;
};
```

### XSS-Schutz
```javascript
// HTML escapen
const escapeHtml = (str) => {
  const div = document.createElement('div');
  div.textContent = str;
  return div.innerHTML;
};

// Verwendung
ui.render(`<h1>${escapeHtml(userInput)}</h1>`, container);
```

## Testing-Strategie

### Manuelle Tests
- [ ] Login/Logout-Flow
- [ ] Turnier erstellen
- [ ] Spieler einschreiben
- [ ] Match-Score eingeben
- [ ] Bracket generieren
- [ ] Echtzeit-Updates
- [ ] OBS-Overlays
- [ ] Responsive Design
- [ ] Error Handling

### Browser-Kompatibilität
- Chrome/Edge (Primary)
- Firefox (Supported)
- Safari (Supported)

## Deployment

### Build-Prozess
1. HTML-Datei optimieren
2. CSS minimieren (Tailwind purge)
3. JavaScript minifizieren
4. Assets optimieren

### Hosting
- Firebase Hosting (empfohlen)
- Statisches Hosting (Alternative)
- CDN für Assets

### Umgebungs-Konfiguration
```javascript
const config = {
  firebase: {
    apiKey: 'YOUR_API_KEY',
    authDomain: 'your-app.firebaseapp.com',
    projectId: 'your-project-id',
    storageBucket: 'your-app.appspot.com',
    messagingSenderId: 'YOUR_SENDER_ID',
    appId: 'YOUR_APP_ID'
  },
  gemini: {
    apiKey: 'YOUR_GEMINI_API_KEY'
  }
};
```

## Wartung & Entwicklung

### Code-Konventionen
- **Namespaces**: Alle Funktionen in Namespaces
- **Naming**: camelCase für Funktionen, PascalCase für Komponenten
- **Comments**: JSDoc für Funktionen
- **Formatting**: 2 Spaces Indentation

### Version Control
- Git für Versionskontrolle
- Feature Branches
- Semantic Versioning

### Dokumentation
- Code-Kommentare
- JSDoc für API-Funktionen
- README für Setup
- CHANGELOG für Änderungen

## Zukünftige Erweiterungen

### Phase 1 (MVP)
- [x] Architektur definiert
- [ ] Basis-UI implementieren
- [ ] Firebase-Integration
- [ ] Turnier-Management
- [ ] Match-Management

### Phase 2
- [ ] OBS-Overlays
- [ ] Statistiken
- [ ] Admin-Panel erweitert
- [ ] Mobile Optimierung

### Phase 3
- [ ] Gemini AI Integration
- [ ] Erweiterte Statistiken
- [ ] Export/Import
- [ ] Multi-Sprachen

### Langfristig
- [ ] Mobile App
- [ ] Live-Streaming Integration
- [ ] Social Features
- [ ] Tournament Templates
- [ ] Advanced Analytics

## Fazit

Die MBS Turnier Manager Architektur ist darauf ausgelegt:
- **Einfachheit**: Single-File, keine Build-Tools nötig
- **Wartbarkeit**: Klare Namespace-Trennung
- **Skalierbarkeit**: Modulare Struktur
- **Performance**: Real-time Updates, optimiertes Rendering
- **Benutzerfreundlichkeit**: Moderne UI, responsive Design

Die Architektur bietet eine solide Grundlage für ein vollständiges Turnier-Management-System mit Raum für zukünftige Erweiterungen.
