# Save Night Feature - Implementation Notes

## Architecture

### Data Model

Two localStorage keys manage all game state:

1. **`the-rail-2026-08-29`** (unchanged)
   - Structure: `{ game: {...}, undo: [...] }`
   - Contains the current live game
   - Never modified by save operations
   - Continues to work exactly as before

2. **`the-rail-saves`** (new)
   - Structure: `[{ id, name, savedAt, game }, ...]`
   - Array of saved game snapshots
   - Each snapshot includes metadata + full game state
   - Independent of current game storage

### View Modes

Three distinct UI modes managed by `viewMode` state variable:

1. **"current"** - Default mode showing live game
   - All buttons enabled
   - Can buy-in, cash-out, add/remove players
   - Undo, Save, Nights, Reset available
   - Updates persist to `the-rail-2026-08-29`

2. **"nights"** - Saved games list view
   - Shows all saved snapshots as cards
   - Tapping a card switches to "viewing-past" mode
   - Back to tonight button returns to "current" mode

3. **"viewing-past"** - Read-only past game view
   - Gold banner indicates viewing mode
   - All action buttons disabled
   - Settlement calculations still shown
   - Back to tonight button returns to "current" mode

## Key Functions

### Save Operations

```javascript
saveCurrentNight(name)
```
- Clones current game with `clone(game)`
- Creates snapshot with metadata (id, name, savedAt, game)
- Prepends to saves array (newest first)
- Writes only to `the-rail-saves` key
- Current game unchanged

### View Switching

```javascript
showMainView()      // Return to current live game
showNightsView()    // Show saved games list
showPastGame(saved) // View a past game snapshot
```

### Rendering

```javascript
publicStateForGame(gameToShow, settleNowFlag)
```
- Replaces old `publicState()`
- Accepts any game object (current or past)
- Calculates totals, settlement, player states
- Used by `refresh()` to render current or past game

## Migration Safety

### Existing Users
- No breaking changes to storage format
- `load()` function unchanged - reads from same key
- If `the-rail-2026-08-29` exists, it loads exactly as before
- New saves feature is purely additive

### New Users
- Both storage keys created on first use
- Current game in `the-rail-2026-08-29`
- Saves array in `the-rail-saves` (empty initially)

## Data Flow

### Saving a Night
1. User clicks Save button
2. Modal prompts for name (default: formatted date)
3. User confirms name
4. `saveCurrentNight()` clones `game` variable
5. Snapshot written to `the-rail-saves`
6. Current game UI unchanged
7. Toast confirms save

### Viewing Past Game
1. User clicks Nights button
2. `showNightsView()` renders list from `loadSaves()`
3. User taps a saved night card
4. `showPastGame()` clones saved game to `viewingGame`
5. UI switches to read-only mode
6. Render shows `viewingGame` instead of `game`
7. Back to tonight restores `game` view

### Back to Current Game
1. User clicks Back to tonight
2. `showMainView()` resets view mode to "current"
3. `viewingGame` set to null
4. `refresh()` renders current `game`
5. All interactive features restored

## Mobile Optimizations

### Touch Targets
- All buttons min 48px height
- Night cards are full-width tap targets
- Modal uses native keyboard types:
  - `inputMode="text"` for save name entry
  - `inputMode="decimal"` for money amounts

### Visual Feedback
- Active states on all interactive elements
- Toast messages for all actions
- Gold banner clearly indicates viewing past game
- Disabled button styling (opacity 0.35)

## Performance

### Memory
- Each saved game: ~1-5KB JSON
- Typical 5-10MB localStorage limit
- Can store 100s of game sessions
- No memory leaks (no event listener cleanup needed)

### Rendering
- Minimal DOM manipulation
- Only re-renders changed sections
- No framework overhead (vanilla JS)

## Edge Cases Handled

1. **Empty game saves** - Allowed, shows $0 and 0 players
2. **Long names** - Truncated at 80 characters
3. **localStorage full** - Graceful error message
4. **Missing saves key** - Returns empty array safely
5. **Corrupted data** - Try/catch prevents crashes
6. **Multiple rapid saves** - Each gets unique ID
7. **Viewing past while live game active** - Completely isolated

## Constraints Met

✅ Never modifies `the-rail-2026-08-29` during save  
✅ Save copies, never clears current game  
✅ Reset still requires confirmation  
✅ Migration safe for existing users  
✅ Single static index.html  
✅ No backend, no npm, no build step  
✅ Vercel deploys to master branch

## Testing Approach

See `TEST_SAVE_FEATURE.md` for comprehensive test scenarios covering:
- Basic save/load
- Multiple saves
- View switching
- Data persistence
- Migration
- Reset behavior
- Edge cases
- Mobile UX

## Future Enhancements (Not Implemented)

Possible future additions (not in scope):
- Delete saved nights
- Rename saved nights
- Export/import saved games
- Search/filter saved nights by date or players
- Save with notes/tags
- Merge two games
- Compare two saved nights

## Code Quality

- Pure JavaScript (no dependencies)
- ~300 lines of new code
- Maintains existing code style
- No breaking changes to existing functions
- Fully backwards compatible
