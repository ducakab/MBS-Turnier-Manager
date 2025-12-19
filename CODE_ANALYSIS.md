# MBS Turnier Manager - Code Analysis & Function Index

## Project Overview
**MBS Turnier Manager** is a Single Page Application (SPA) for managing pool billiards tournaments. The application is designed as a single HTML file containing all functionality.

### Technology Stack
- **Frontend**: Vanilla JavaScript (ES6+), HTML5
- **Styling**: Tailwind CSS with Glass/Neon design system
- **Backend**: Firebase 11.6.1 (Authentication, Firestore, Real-time Database)
- **Icons**: FontAwesome
- **Effects**: Confetti.js
- **AI Integration**: Google Gemini API
- **Responsive**: Optimized for Tablet and Desktop

### Design System
- **Primary Background**: Dark (#050505)
- **Accent Colors**:
  - Green: Success states, active elements
  - Blue-Purple: Primary actions, highlights
  - Red: Alerts, deletions, warnings
- **Components**:
  - `.glass-panel`: Glassmorphism effect panels
  - Button classes: Various styled buttons
  - Responsive breakpoints for tablet/desktop

## Architecture

### Single-File Structure
The application follows a single-file architecture with clear namespace separation:

```
index.html
├── HTML Structure
├── <style> - Tailwind + Custom CSS
└── <script> - Application Logic
    ├── app namespace   - Core application
    ├── ui namespace    - UI components
    └── logic namespace - Business logic
```

### State Management
- **Central State**: Single source of truth
- **Real-time Sync**: Firebase onSnapshot for live updates
- **State Flow**: Unidirectional data flow

## Function Index

### 1. App Namespace (`app.*`)
Core application initialization and lifecycle management.

#### 1.1 Initialization Functions
```javascript
app.init()
```
- **Purpose**: Initialize the entire application
- **Responsibilities**:
  - Load configuration
  - Initialize Firebase
  - Set up authentication listeners
  - Initialize routing
  - Render initial UI
- **Dependencies**: Firebase SDK, UI components

```javascript
app.loadConfig()
```
- **Purpose**: Load application configuration
- **Returns**: Configuration object
- **Config includes**: Firebase keys, API endpoints, feature flags

```javascript
app.setupFirebase()
```
- **Purpose**: Initialize Firebase services
- **Services**: Auth, Firestore, Real-time Database
- **Setup**: Connection, listeners, error handlers

#### 1.2 State Management Functions
```javascript
app.state.init()
```
- **Purpose**: Initialize central state object
- **State structure**:
  - `user`: Current user data
  - `tournaments`: Active tournaments
  - `matches`: Current matches
  - `players`: Player roster
  - `settings`: App settings
  - `ui`: UI state (modals, loading, etc.)

```javascript
app.state.get(key)
```
- **Purpose**: Get state value by key
- **Parameters**: `key` (string) - State property path
- **Returns**: State value

```javascript
app.state.set(key, value)
```
- **Purpose**: Update state value
- **Parameters**: 
  - `key` (string) - State property path
  - `value` (any) - New value
- **Side effects**: Triggers UI updates

```javascript
app.state.subscribe(key, callback)
```
- **Purpose**: Subscribe to state changes
- **Parameters**:
  - `key` (string) - State property to watch
  - `callback` (function) - Called on change
- **Returns**: Unsubscribe function

#### 1.3 Routing Functions
```javascript
app.router.init()
```
- **Purpose**: Initialize client-side routing
- **Setup**: Hash-based routing, route handlers

```javascript
app.router.navigate(path)
```
- **Purpose**: Navigate to a route
- **Parameters**: `path` (string) - Route path
- **Side effects**: Updates URL, renders new view

```javascript
app.router.register(path, handler)
```
- **Purpose**: Register route handler
- **Parameters**:
  - `path` (string) - Route pattern
  - `handler` (function) - Route handler function

#### 1.4 Authentication Functions
```javascript
app.auth.init()
```
- **Purpose**: Initialize authentication system
- **Setup**: Firebase Auth, listeners

```javascript
app.auth.login(email, password)
```
- **Purpose**: User login
- **Parameters**: Email and password
- **Returns**: Promise<User>

```javascript
app.auth.logout()
```
- **Purpose**: User logout
- **Returns**: Promise<void>

```javascript
app.auth.getCurrentUser()
```
- **Purpose**: Get current authenticated user
- **Returns**: User object or null

```javascript
app.auth.checkAdmin()
```
- **Purpose**: Check if current user has admin rights
- **Returns**: Boolean

### 2. UI Namespace (`ui.*`)
User interface components and rendering logic.

#### 2.1 Core UI Functions
```javascript
ui.render(component, container)
```
- **Purpose**: Render component to container
- **Parameters**:
  - `component` (string|HTMLElement) - Component to render
  - `container` (HTMLElement) - Target container

```javascript
ui.update(selector, content)
```
- **Purpose**: Update specific UI element
- **Parameters**:
  - `selector` (string) - CSS selector
  - `content` (string|HTMLElement) - New content

```javascript
ui.clear(container)
```
- **Purpose**: Clear container contents
- **Parameters**: `container` (HTMLElement|string)

#### 2.2 View Components
```javascript
ui.views.dashboard()
```
- **Purpose**: Render main dashboard view
- **Returns**: Dashboard HTML

```javascript
ui.views.tournamentList()
```
- **Purpose**: Render tournament list view
- **Returns**: Tournament list HTML

```javascript
ui.views.tournamentDetail(tournamentId)
```
- **Purpose**: Render tournament detail view
- **Parameters**: `tournamentId` (string)
- **Returns**: Tournament detail HTML

```javascript
ui.views.matchView(matchId)
```
- **Purpose**: Render match view
- **Parameters**: `matchId` (string)
- **Returns**: Match view HTML

```javascript
ui.views.scoreboard(tournamentId)
```
- **Purpose**: Render scoreboard view
- **Parameters**: `tournamentId` (string)
- **Returns**: Scoreboard HTML

```javascript
ui.views.adminPanel()
```
- **Purpose**: Render admin control panel
- **Returns**: Admin panel HTML
- **Requires**: Admin authentication

```javascript
ui.views.obsOverlay(mode)
```
- **Purpose**: Render OBS overlay
- **Parameters**: `mode` (string) - Overlay type (scoreboard, match, bracket)
- **Returns**: OBS overlay HTML

#### 2.3 Component Functions
```javascript
ui.components.header(user)
```
- **Purpose**: Render header component
- **Parameters**: `user` (object) - Current user
- **Returns**: Header HTML

```javascript
ui.components.navigation(currentRoute)
```
- **Purpose**: Render navigation menu
- **Parameters**: `currentRoute` (string)
- **Returns**: Navigation HTML

```javascript
ui.components.tournamentCard(tournament)
```
- **Purpose**: Render tournament card
- **Parameters**: `tournament` (object)
- **Returns**: Card HTML

```javascript
ui.components.matchCard(match)
```
- **Purpose**: Render match card
- **Parameters**: `match` (object)
- **Returns**: Match card HTML

```javascript
ui.components.playerCard(player)
```
- **Purpose**: Render player card
- **Parameters**: `player` (object)
- **Returns**: Player card HTML

```javascript
ui.components.scoreDisplay(score)
```
- **Purpose**: Render score display
- **Parameters**: `score` (object)
- **Returns**: Score display HTML

```javascript
ui.components.bracketView(bracket)
```
- **Purpose**: Render tournament bracket
- **Parameters**: `bracket` (object)
- **Returns**: Bracket visualization HTML

#### 2.4 Modal Functions
```javascript
ui.modal.open(config)
```
- **Purpose**: Open modal dialog
- **Parameters**: `config` (object) - Modal configuration
  - `title` (string)
  - `content` (string|HTMLElement)
  - `actions` (array) - Button configurations

```javascript
ui.modal.close()
```
- **Purpose**: Close current modal

```javascript
ui.modal.confirm(message)
```
- **Purpose**: Show confirmation dialog
- **Parameters**: `message` (string)
- **Returns**: Promise<boolean>

```javascript
ui.modal.alert(message, type)
```
- **Purpose**: Show alert message
- **Parameters**:
  - `message` (string)
  - `type` (string) - 'success', 'error', 'warning', 'info'

#### 2.5 Form Functions
```javascript
ui.forms.createTournament()
```
- **Purpose**: Render tournament creation form
- **Returns**: Form HTML

```javascript
ui.forms.editTournament(tournamentId)
```
- **Purpose**: Render tournament edit form
- **Parameters**: `tournamentId` (string)
- **Returns**: Form HTML

```javascript
ui.forms.addPlayer()
```
- **Purpose**: Render add player form
- **Returns**: Form HTML

```javascript
ui.forms.matchScore(matchId)
```
- **Purpose**: Render match score entry form
- **Parameters**: `matchId` (string)
- **Returns**: Form HTML

```javascript
ui.forms.validate(formData, rules)
```
- **Purpose**: Validate form data
- **Parameters**:
  - `formData` (object)
  - `rules` (object) - Validation rules
- **Returns**: Validation result object

#### 2.6 Loading & Feedback
```javascript
ui.loading.show(message)
```
- **Purpose**: Show loading indicator
- **Parameters**: `message` (string) - Optional loading message

```javascript
ui.loading.hide()
```
- **Purpose**: Hide loading indicator

```javascript
ui.toast.show(message, type, duration)
```
- **Purpose**: Show toast notification
- **Parameters**:
  - `message` (string)
  - `type` (string) - 'success', 'error', 'warning', 'info'
  - `duration` (number) - Display duration in ms

```javascript
ui.confetti.celebrate()
```
- **Purpose**: Trigger confetti celebration effect
- **Use cases**: Match win, tournament complete

### 3. Logic Namespace (`logic.*`)
Business logic and data operations.

#### 3.1 Tournament Logic
```javascript
logic.tournament.create(data)
```
- **Purpose**: Create new tournament
- **Parameters**: `data` (object) - Tournament data
- **Returns**: Promise<Tournament>
- **Validation**: Required fields, date ranges

```javascript
logic.tournament.update(id, data)
```
- **Purpose**: Update tournament
- **Parameters**:
  - `id` (string)
  - `data` (object) - Updated fields
- **Returns**: Promise<Tournament>

```javascript
logic.tournament.delete(id)
```
- **Purpose**: Delete tournament
- **Parameters**: `id` (string)
- **Returns**: Promise<void>

```javascript
logic.tournament.get(id)
```
- **Purpose**: Get tournament by ID
- **Parameters**: `id` (string)
- **Returns**: Promise<Tournament>

```javascript
logic.tournament.list(filters)
```
- **Purpose**: List tournaments
- **Parameters**: `filters` (object) - Optional filters
- **Returns**: Promise<Tournament[]>

```javascript
logic.tournament.start(id)
```
- **Purpose**: Start tournament
- **Parameters**: `id` (string)
- **Returns**: Promise<void>
- **Side effects**: Generates bracket, schedules matches

```javascript
logic.tournament.complete(id)
```
- **Purpose**: Complete tournament
- **Parameters**: `id` (string)
- **Returns**: Promise<void>
- **Side effects**: Calculates final standings, awards

#### 3.2 Match Logic
```javascript
logic.match.create(tournamentId, player1, player2)
```
- **Purpose**: Create new match
- **Parameters**:
  - `tournamentId` (string)
  - `player1` (string)
  - `player2` (string)
- **Returns**: Promise<Match>

```javascript
logic.match.updateScore(matchId, score)
```
- **Purpose**: Update match score
- **Parameters**:
  - `matchId` (string)
  - `score` (object) - Score data
- **Returns**: Promise<Match>

```javascript
logic.match.complete(matchId, winnerId)
```
- **Purpose**: Complete match
- **Parameters**:
  - `matchId` (string)
  - `winnerId` (string)
- **Returns**: Promise<Match>
- **Side effects**: Updates bracket, schedules next match

```javascript
logic.match.get(id)
```
- **Purpose**: Get match by ID
- **Parameters**: `id` (string)
- **Returns**: Promise<Match>

```javascript
logic.match.listByTournament(tournamentId)
```
- **Purpose**: List matches for tournament
- **Parameters**: `tournamentId` (string)
- **Returns**: Promise<Match[]>

#### 3.3 Player Logic
```javascript
logic.player.create(data)
```
- **Purpose**: Create player profile
- **Parameters**: `data` (object) - Player data
- **Returns**: Promise<Player>

```javascript
logic.player.update(id, data)
```
- **Purpose**: Update player profile
- **Parameters**:
  - `id` (string)
  - `data` (object)
- **Returns**: Promise<Player>

```javascript
logic.player.get(id)
```
- **Purpose**: Get player by ID
- **Parameters**: `id` (string)
- **Returns**: Promise<Player>

```javascript
logic.player.list(filters)
```
- **Purpose**: List players
- **Parameters**: `filters` (object)
- **Returns**: Promise<Player[]>

```javascript
logic.player.getStats(playerId)
```
- **Purpose**: Get player statistics
- **Parameters**: `playerId` (string)
- **Returns**: Promise<Stats>
- **Stats include**: Win/loss record, average score, ranking

```javascript
logic.player.enroll(playerId, tournamentId)
```
- **Purpose**: Enroll player in tournament
- **Parameters**:
  - `playerId` (string)
  - `tournamentId` (string)
- **Returns**: Promise<void>

#### 3.4 Bracket Logic
```javascript
logic.bracket.generate(tournamentId, players)
```
- **Purpose**: Generate tournament bracket
- **Parameters**:
  - `tournamentId` (string)
  - `players` (array) - List of player IDs
- **Returns**: Promise<Bracket>
- **Algorithms**: Single elimination, double elimination, round robin

```javascript
logic.bracket.update(tournamentId, matchResult)
```
- **Purpose**: Update bracket after match
- **Parameters**:
  - `tournamentId` (string)
  - `matchResult` (object)
- **Returns**: Promise<Bracket>

```javascript
logic.bracket.get(tournamentId)
```
- **Purpose**: Get tournament bracket
- **Parameters**: `tournamentId` (string)
- **Returns**: Promise<Bracket>

#### 3.5 Scoring Logic
```javascript
logic.scoring.calculate(matchData)
```
- **Purpose**: Calculate match score
- **Parameters**: `matchData` (object)
- **Returns**: Score object
- **Rules**: Pool billiards scoring rules

```javascript
logic.scoring.validateScore(score)
```
- **Purpose**: Validate score data
- **Parameters**: `score` (object)
- **Returns**: Boolean

```javascript
logic.scoring.getRankings(tournamentId)
```
- **Purpose**: Calculate tournament rankings
- **Parameters**: `tournamentId` (string)
- **Returns**: Promise<Ranking[]>

#### 3.6 Statistics Logic
```javascript
logic.stats.calculatePlayerStats(playerId)
```
- **Purpose**: Calculate player statistics
- **Parameters**: `playerId` (string)
- **Returns**: Promise<Stats>

```javascript
logic.stats.getTournamentStats(tournamentId)
```
- **Purpose**: Get tournament statistics
- **Parameters**: `tournamentId` (string)
- **Returns**: Promise<Stats>

```javascript
logic.stats.getLeaderboard()
```
- **Purpose**: Get global leaderboard
- **Returns**: Promise<Leaderboard>

### 4. Firebase Integration (`firebase.*`)

#### 4.1 Database Functions
```javascript
firebase.db.collection(name)
```
- **Purpose**: Get Firestore collection reference
- **Parameters**: `name` (string) - Collection name
- **Returns**: Collection reference

```javascript
firebase.db.doc(path)
```
- **Purpose**: Get Firestore document reference
- **Parameters**: `path` (string) - Document path
- **Returns**: Document reference

```javascript
firebase.db.get(path)
```
- **Purpose**: Get document data
- **Parameters**: `path` (string)
- **Returns**: Promise<Data>

```javascript
firebase.db.set(path, data)
```
- **Purpose**: Set document data
- **Parameters**:
  - `path` (string)
  - `data` (object)
- **Returns**: Promise<void>

```javascript
firebase.db.update(path, data)
```
- **Purpose**: Update document fields
- **Parameters**:
  - `path` (string)
  - `data` (object)
- **Returns**: Promise<void>

```javascript
firebase.db.delete(path)
```
- **Purpose**: Delete document
- **Parameters**: `path` (string)
- **Returns**: Promise<void>

```javascript
firebase.db.query(collection, filters)
```
- **Purpose**: Query collection
- **Parameters**:
  - `collection` (string)
  - `filters` (array) - Query filters
- **Returns**: Promise<QuerySnapshot>

#### 4.2 Real-time Listeners
```javascript
firebase.listeners.onSnapshot(path, callback)
```
- **Purpose**: Listen to document changes
- **Parameters**:
  - `path` (string)
  - `callback` (function) - Called on changes
- **Returns**: Unsubscribe function

```javascript
firebase.listeners.onCollectionSnapshot(collection, callback)
```
- **Purpose**: Listen to collection changes
- **Parameters**:
  - `collection` (string)
  - `callback` (function)
- **Returns**: Unsubscribe function

```javascript
firebase.listeners.cleanup()
```
- **Purpose**: Remove all active listeners

#### 4.3 Authentication
```javascript
firebase.auth.signIn(email, password)
```
- **Purpose**: Sign in user
- **Returns**: Promise<User>

```javascript
firebase.auth.signOut()
```
- **Purpose**: Sign out user
- **Returns**: Promise<void>

```javascript
firebase.auth.onAuthStateChanged(callback)
```
- **Purpose**: Listen to auth state changes
- **Parameters**: `callback` (function)
- **Returns**: Unsubscribe function

### 5. Gemini AI Integration (`gemini.*`)

#### 5.1 AI Functions
```javascript
gemini.init(apiKey)
```
- **Purpose**: Initialize Gemini API
- **Parameters**: `apiKey` (string)

```javascript
gemini.generateMatchCommentary(matchData)
```
- **Purpose**: Generate AI match commentary
- **Parameters**: `matchData` (object)
- **Returns**: Promise<string>

```javascript
gemini.analyzeTournament(tournamentId)
```
- **Purpose**: Generate tournament analysis
- **Parameters**: `tournamentId` (string)
- **Returns**: Promise<Analysis>

```javascript
gemini.predictOutcome(match)
```
- **Purpose**: Predict match outcome
- **Parameters**: `match` (object)
- **Returns**: Promise<Prediction>

```javascript
gemini.generatePlayerProfile(playerId)
```
- **Purpose**: Generate AI player profile description
- **Parameters**: `playerId` (string)
- **Returns**: Promise<string>

### 6. Utility Functions (`utils.*`)

#### 6.1 Data Utilities
```javascript
utils.formatDate(date, format)
```
- **Purpose**: Format date string
- **Parameters**:
  - `date` (Date|string)
  - `format` (string)
- **Returns**: Formatted date string

```javascript
utils.formatTime(time)
```
- **Purpose**: Format time string
- **Parameters**: `time` (Date|string)
- **Returns**: Formatted time string

```javascript
utils.generateId()
```
- **Purpose**: Generate unique ID
- **Returns**: UUID string

```javascript
utils.debounce(func, delay)
```
- **Purpose**: Debounce function calls
- **Parameters**:
  - `func` (function)
  - `delay` (number)
- **Returns**: Debounced function

```javascript
utils.throttle(func, limit)
```
- **Purpose**: Throttle function calls
- **Parameters**:
  - `func` (function)
  - `limit` (number)
- **Returns**: Throttled function

#### 6.2 DOM Utilities
```javascript
utils.dom.select(selector)
```
- **Purpose**: Select DOM element
- **Parameters**: `selector` (string)
- **Returns**: HTMLElement

```javascript
utils.dom.selectAll(selector)
```
- **Purpose**: Select all matching elements
- **Parameters**: `selector` (string)
- **Returns**: NodeList

```javascript
utils.dom.createElement(tag, attrs, children)
```
- **Purpose**: Create DOM element
- **Parameters**:
  - `tag` (string)
  - `attrs` (object)
  - `children` (array)
- **Returns**: HTMLElement

```javascript
utils.dom.addClass(element, className)
```
- **Purpose**: Add class to element
- **Parameters**:
  - `element` (HTMLElement)
  - `className` (string)

```javascript
utils.dom.removeClass(element, className)
```
- **Purpose**: Remove class from element
- **Parameters**:
  - `element` (HTMLElement)
  - `className` (string)

#### 6.3 Validation Utilities
```javascript
utils.validate.email(email)
```
- **Purpose**: Validate email address
- **Parameters**: `email` (string)
- **Returns**: Boolean

```javascript
utils.validate.required(value)
```
- **Purpose**: Check if value is not empty
- **Parameters**: `value` (any)
- **Returns**: Boolean

```javascript
utils.validate.minLength(value, min)
```
- **Purpose**: Check minimum length
- **Parameters**:
  - `value` (string)
  - `min` (number)
- **Returns**: Boolean

```javascript
utils.validate.number(value)
```
- **Purpose**: Check if value is number
- **Parameters**: `value` (any)
- **Returns**: Boolean

#### 6.4 Storage Utilities
```javascript
utils.storage.set(key, value)
```
- **Purpose**: Store data in localStorage
- **Parameters**:
  - `key` (string)
  - `value` (any)

```javascript
utils.storage.get(key)
```
- **Purpose**: Get data from localStorage
- **Parameters**: `key` (string)
- **Returns**: Stored value

```javascript
utils.storage.remove(key)
```
- **Purpose**: Remove data from localStorage
- **Parameters**: `key` (string)

```javascript
utils.storage.clear()
```
- **Purpose**: Clear all localStorage

### 7. OBS Overlay Functions (`obs.*`)

#### 7.1 Overlay Management
```javascript
obs.init(mode)
```
- **Purpose**: Initialize OBS overlay mode
- **Parameters**: `mode` (string) - Overlay type

```javascript
obs.scoreboard.show(matchId)
```
- **Purpose**: Show scoreboard overlay
- **Parameters**: `matchId` (string)

```javascript
obs.scoreboard.update(score)
```
- **Purpose**: Update scoreboard data
- **Parameters**: `score` (object)

```javascript
obs.bracket.show(tournamentId)
```
- **Purpose**: Show bracket overlay
- **Parameters**: `tournamentId` (string)

```javascript
obs.playerInfo.show(playerId)
```
- **Purpose**: Show player info overlay
- **Parameters**: `playerId` (string)

```javascript
obs.transition(effect)
```
- **Purpose**: Trigger overlay transition effect
- **Parameters**: `effect` (string) - Transition type

## Data Models

### Tournament
```javascript
{
  id: string,
  name: string,
  date: Date,
  type: 'single-elimination' | 'double-elimination' | 'round-robin',
  status: 'upcoming' | 'in-progress' | 'completed',
  players: string[], // player IDs
  matches: string[], // match IDs
  bracket: object,
  settings: object,
  createdBy: string,
  createdAt: Date,
  updatedAt: Date
}
```

### Match
```javascript
{
  id: string,
  tournamentId: string,
  player1Id: string,
  player2Id: string,
  score: {
    player1: number,
    player2: number
  },
  status: 'scheduled' | 'in-progress' | 'completed',
  winnerId: string | null,
  round: number,
  bracketPosition: string,
  startTime: Date | null,
  endTime: Date | null,
  createdAt: Date,
  updatedAt: Date
}
```

### Player
```javascript
{
  id: string,
  name: string,
  email: string,
  avatar: string | null,
  stats: {
    matchesPlayed: number,
    matchesWon: number,
    matchesLost: number,
    tournamentsPlayed: number,
    tournamentsWon: number,
    ranking: number
  },
  createdAt: Date,
  updatedAt: Date
}
```

### User
```javascript
{
  id: string,
  email: string,
  displayName: string,
  role: 'admin' | 'user',
  createdAt: Date,
  lastLogin: Date
}
```

## Event Listeners

### Application Events
- `app:init` - Application initialized
- `app:ready` - Application ready for interaction
- `auth:login` - User logged in
- `auth:logout` - User logged out
- `route:change` - Route changed

### Tournament Events
- `tournament:created` - Tournament created
- `tournament:updated` - Tournament updated
- `tournament:started` - Tournament started
- `tournament:completed` - Tournament completed

### Match Events
- `match:created` - Match created
- `match:started` - Match started
- `match:score-updated` - Score updated
- `match:completed` - Match completed

### UI Events
- `modal:open` - Modal opened
- `modal:close` - Modal closed
- `toast:show` - Toast notification shown

## CSS Classes

### Layout Classes
- `.glass-panel` - Glassmorphism panel
- `.container` - Main container
- `.grid-layout` - Grid layout
- `.flex-layout` - Flexbox layout

### Button Classes
- `.btn` - Base button
- `.btn-primary` - Primary action (blue-purple)
- `.btn-success` - Success action (green)
- `.btn-danger` - Destructive action (red)
- `.btn-secondary` - Secondary action
- `.btn-ghost` - Ghost/transparent button
- `.btn-icon` - Icon-only button

### Component Classes
- `.card` - Card component
- `.tournament-card` - Tournament card
- `.match-card` - Match card
- `.player-card` - Player card
- `.score-display` - Score display
- `.bracket-view` - Bracket visualization

### State Classes
- `.loading` - Loading state
- `.disabled` - Disabled state
- `.active` - Active state
- `.selected` - Selected state
- `.error` - Error state

### Responsive Classes
- `.tablet:*` - Tablet breakpoint
- `.desktop:*` - Desktop breakpoint

## Firebase Collections

### Collections Structure
```
/tournaments
  /{tournamentId}
    - Tournament data
    /matches
      /{matchId} - Match data
    /enrollments
      /{playerId} - Enrollment data

/players
  /{playerId}
    - Player data
    /stats
      - Statistics data

/users
  /{userId}
    - User data

/settings
  /app
    - Application settings
```

## API Endpoints (Gemini)

### Gemini API Integration
- **Endpoint**: `https://generativelanguage.googleapis.com/v1/models/gemini-pro`
- **Authentication**: API Key
- **Rate Limits**: Consider caching and throttling

## Performance Considerations

### Optimization Strategies
1. **Lazy Loading**: Load components on demand
2. **Debouncing**: Debounce search and filter inputs
3. **Caching**: Cache frequently accessed data
4. **Real-time Optimization**: Unsubscribe from unused listeners
5. **Bundle Size**: Keep single file optimized (<500KB)

### Real-time Data Flow
```
Firebase Firestore
  ↓ (onSnapshot)
State Management
  ↓ (state.set)
UI Update
  ↓ (ui.render)
DOM Update
```

## Security Considerations

### Firebase Security Rules
- Authenticated users can read tournaments
- Only admins can create/update/delete tournaments
- Users can only update their own player profiles
- Match scores can only be updated by admins or match participants

### Input Validation
- Validate all user inputs
- Sanitize data before Firebase operations
- Validate scores against game rules
- Check permissions before admin operations

## Development Workflow

### Local Development
1. Open `index.html` in browser
2. Use browser DevTools for debugging
3. Firebase Emulators for local testing (optional)

### Deployment
1. Deploy single HTML file to hosting
2. Configure Firebase project
3. Set up Gemini API key
4. Configure environment variables

## Testing Strategy

### Manual Testing Checklist
- [ ] Authentication flow
- [ ] Tournament creation
- [ ] Player enrollment
- [ ] Match scoring
- [ ] Bracket generation
- [ ] Real-time updates
- [ ] OBS overlays
- [ ] Responsive design
- [ ] Error handling

### Browser Compatibility
- Chrome/Edge (Chromium) - Primary
- Firefox - Supported
- Safari - Supported
- Mobile browsers - Not primary focus

## Future Enhancements

### Potential Features
1. Live streaming integration
2. Mobile app version
3. Advanced statistics and analytics
4. Tournament templates
5. Multi-language support
6. Export/import functionality
7. Tournament history archive
8. Player profiles with photos
9. Social media integration
10. Email notifications

## Conclusion

This document provides a comprehensive analysis and function index for the MBS Turnier Manager project. The architecture is designed for maintainability, scalability, and real-time performance while keeping the single-file constraint.

### Key Strengths
- **Single-file simplicity**: Easy deployment and maintenance
- **Real-time updates**: Live tournament and match updates
- **Modern design**: Glass/neon aesthetic with dark theme
- **Flexible architecture**: Clear namespace separation
- **AI enhancement**: Gemini API for advanced features

### Development Priorities
1. Core tournament and match management
2. Real-time synchronization
3. Admin panel functionality
4. Scoreboard and OBS overlays
5. UI polish and responsive design
6. AI features integration

**Status**: Architecture analyzed, functions indexed, ready for implementation.
