# PNL Summary View - User Guide

## What It Does

The PNL (Profit and Loss) Summary is a clear, scannable table that shows each player's final results when the game is ready to settle.

## When It Appears

The PNL summary automatically shows when:
- ✅ **Everyone has cashed out**, OR
- ✅ **You pressed "Settle now"**

It stays hidden during active play so the live cashier cards remain visible.

## What You See

### During Active Game (PNL Hidden)
```
┌─────────────────────────┐
│ Sherry              OUT │
│ Buy-in   Cash-out   Net │
│  $200      $350    +$150│
│ [Sit back] [Update]     │
└─────────────────────────┘

┌─────────────────────────┐
│ Ken                  IN │
│ Buy-in   Cash-out   Net │
│  $150      $110     open│
│ [Buy-in]  [Cash out]    │
└─────────────────────────┘

... more seat cards ...
```

### After Ready to Settle (PNL Shows)
```
┌─ Final PNL ────────────────────────────────┐
│                                            │
│ Player    │  Buy-in  │ Cash-out │    Net  │
│───────────┼──────────┼──────────┼─────────│
│ Sherry    │    $200  │    $350  │  +$150  │ ← Green
│ Ken       │    $150  │    $110  │   -$40  │ ← Red
│ Becky     │    $200  │    $220  │   +$20  │ ← Green
│ Wayne     │    $100  │    $140  │   +$40  │ ← Green
│───────────┼──────────┼──────────┼─────────│
│ Total     │    $650  │    $820  │  +$170  │
└────────────────────────────────────────────┘

Settlement
─────────────────────────────
Ken pays Sherry     $40
```

## Color Coding

| Color         | Meaning              | Example    |
|---------------|----------------------|------------|
| 🟢 **Green**  | Won money (profit)   | +$150      |
| 🔴 **Red**    | Lost money           | -$40       |
| ⚪ **Gray**   | Break-even or $0     | $0         |

## Reading the Table

### Player Rows
Each row shows one player who bought in:
- **Player**: Name
- **Buy-in**: Total chips purchased
- **Cash-out**: Total chips returned
- **Net**: Profit (+) or Loss (-)

### Totals Row
Bottom row shows the house totals:
- **Buy-in column**: All money that went in
- **Cash-out column**: All money paid out
- **Net column**: Money still on table (should be $0 when balanced)

## Example Scenarios

### Scenario 1: Balanced Table
```
Final PNL
Alice    $200  →  $250  =  +$50  (green)
Bob      $200  →  $150  =  -$50  (red)
Total    $400  →  $400  =   $0   (balanced ✓)

Settlement: Bob pays Alice $50
```

### Scenario 2: Someone Still In (Settle Now)
```
Final PNL
Alice    $200  →  $300  =  +$100  (green)
Bob      $200  →  $100  =  -$100  (red)
Charlie  $200  →    $0  =  -$200  (red, walked with $0)
Total    $600  →  $400  =  -$200

Settlement:
Bob pays Alice $100
Charlie pays Alice $200
```

### Scenario 3: Everyone Break-Even
```
Final PNL
Alice    $100  →  $100  =   $0   (gray)
Bob      $100  →  $100  =   $0   (gray)
Total    $200  →  $200  =   $0

Settlement: Even table — no payments needed.
```

## FAQ

### Q: Why don't I see the PNL summary?
**A:** The summary only appears when:
1. Everyone who bought in has cashed out, OR
2. You pressed "Settle now"

If people are still playing, you'll see the normal seat cards instead.

### Q: Can I see PNL for past games?
**A:** Yes! When you view a saved night (after the Save night feature is merged), the PNL summary will show if that game was settled.

### Q: Does this replace the settlement payments?
**A:** No! The PNL summary shows **who won/lost**. The settlement section below it shows **who pays whom**. Both are useful:
- **PNL**: See final results at a glance
- **Settlement**: Know which Venmo/cash payments to make

### Q: What if someone didn't buy in?
**A:** Players who didn't buy in (seated but no chips purchased) are excluded from the PNL table. They don't affect the game finances.

### Q: What does the totals row mean?
**A:** The totals row shows:
- **Buy-in**: Sum of all chips purchased
- **Cash-out**: Sum of all chips returned
- **Net**: Difference (should be $0 when books balance)

If the net is not $0 when everyone has cashed out, there's a discrepancy to investigate.

## Mobile View

The PNL table is optimized for phone screens:
- Compact but readable text sizes
- Proper spacing for fat fingers
- Scrolls horizontally if needed
- Matches the felt-green design

## Technical Notes

- **No extra buttons**: Appears automatically when ready
- **No extra taps**: Just cash everyone out as usual
- **No localStorage changes**: Uses existing game data
- **No performance impact**: Lightweight table rendering

## When to Use Each View

| View              | When to Use                           |
|-------------------|---------------------------------------|
| Seat Cards        | During active play                    |
| PNL Summary       | To see final profit/loss results      |
| Settlement List   | To know who pays whom (Venmo/cash)    |

All three views work together to give you the complete picture of your poker night finances.
