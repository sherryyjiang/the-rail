# Save Night Feature - Test Scenarios

## Test 1: Save Current Game (Basic)
1. Open The Rail with active game (players, buy-ins, cash-outs)
2. Click **Save** button
3. Modal appears with suggested name "Sat 29 Aug 2026"
4. Edit name to "Friday Game" and confirm
5. ✅ Toast shows "Night saved as 'Friday Game'"
6. ✅ Current game still visible on screen
7. ✅ All players and totals unchanged

## Test 2: View Saved Nights List
1. Click **Nights** button
2. ✅ See list of saved nights with:
   - Name ("Friday Game")
   - Saved timestamp
   - Money in amount
   - Player count
   - Game date
3. Click **Back to tonight**
4. ✅ Returns to current game view

## Test 3: View Past Game (Read-Only)
1. Click **Nights** → select a saved night
2. ✅ Gold banner shows "Viewing past night"
3. ✅ All player cards displayed with correct data
4. ✅ Buy-in/Cash-out buttons are disabled
5. ✅ Remove button disabled
6. ✅ Add player form hidden
7. ✅ Settle now button disabled
8. ✅ Reset night button hidden
9. ✅ Save button hidden
10. ✅ Undo button hidden
11. ✅ Settlement calculations shown correctly
12. Click **Back to tonight**
13. ✅ Returns to current game with all interactive features restored

## Test 4: Multiple Saves
1. Save current game as "Game 1"
2. Make changes (add player, buy-in)
3. Save again as "Game 2"
4. ✅ Both games appear in Nights list
5. ✅ Each snapshot is independent
6. ✅ Current game still has latest changes

## Test 5: Data Persistence
1. Save a game
2. Close browser tab
3. Open The Rail again
4. ✅ Current game restored from localStorage
5. Click **Nights**
6. ✅ Saved games still present
7. ✅ No data loss

## Test 6: Migration (Existing Users)
1. Setup: Create localStorage entry for `the-rail-2026-08-29` with game data
2. Open updated The Rail
3. ✅ Existing game loads correctly
4. ✅ All players and money visible
5. ✅ Can continue playing (buy-in, cash-out work)
6. ✅ New Save/Nights buttons appear
7. ✅ No data corruption

## Test 7: Reset Night (Confirmation Still Works)
1. Make changes to current game
2. Click **Reset night**
3. ✅ Confirmation dialog appears
4. Cancel
5. ✅ Game unchanged
6. Click **Reset night** again, confirm
7. ✅ Current game cleared
8. ✅ Saved nights still intact in Nights list

## Test 8: Edge Cases

### Empty Game Save
1. Fresh page, no players
2. Click **Save**
3. ✅ Can save empty game
4. ✅ Shows in Nights list with $0 and 0 players

### Long Name
1. Try to save with 100+ character name
2. ✅ Toast shows "Name is too long"

### Empty Name
1. Try to save with empty/whitespace name
2. ✅ Toast shows "Name is required"

### localStorage Full
1. Fill localStorage to capacity
2. Try to save
3. ✅ Toast shows "Couldn't save on this device"
4. ✅ App continues working

## Browser Compatibility
- ✅ Chrome/Edge (desktop & mobile)
- ✅ Safari (desktop & iOS)
- ✅ Firefox
- ✅ All require localStorage support (graceful degradation if disabled)

## Performance
- Saved games stored as JSON in localStorage
- Each save ~1-5KB depending on player count
- Typical browser localStorage limit: 5-10MB
- Can store hundreds of game sessions

## Security
- No server communication
- All data stays in user's browser
- Clearing browser data removes all games
- No PII collected or transmitted
