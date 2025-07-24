# Flowgen MVP Status Assessment

## Current State: NOT MVP READY

### What Works
- Screenshot upload interface
- OCR text extraction (Google Vision API)
- Platform detection (Uber Eats vs DoorDash)
- Basic route calculation API calls
- Database storage of offers and decisions

### What's Broken (Critical)

#### 1. Location Resolution Pipeline - BROKEN
**Problem**: OCR extracts "Little Caesars" but Google Places API integration doesn't work
**Impact**: Routes calculated to wrong coordinates or fail entirely
**Status**: Google Places service exists but isn't properly integrated with DoorDash processor

#### 2. Route Time Calculation - BROKEN  
**Problem**: Shows "0 minutes added" for opposite-direction trips
**Impact**: Drivers accept money-losing offers thinking they're efficient
**Status**: Backtrack detection logic exists but fails in practice

### Root Cause Analysis

#### Location Resolution Flow (What Should Happen vs Reality)
**Should Happen:**
```
OCR: "Little Caesars" + map streets → Google Places: "Little Caesars near Clark & Division Chicago" → Result: "1224 N Clark St" → Route calculation works
```

**Reality:**
```
OCR: "Little Caesars" → System: "Restaurant location" → Google Maps fails → Route calculation impossible
```

#### Route Calculation Flow (What Should Happen vs Reality)
**Should Happen:**
```
Calculate 4 routes → Compare times → Show realistic added time (15-45 minutes)
```

**Reality:**
```
Calculate 4 routes → Opposite direction returns 0 minutes → Driver gets wrong recommendation
```

## Technical Debt Blocking MVP

### 1. DoorDash Map Processor
**File**: `server/doordash-map-processor.ts`
**Issue**: Has Google Places service but `processDoorDashOffer` method is static and doesn't use it
**Fix Required**: Make method non-static, integrate Google Places lookup

### 2. Route Optimization Logic
**File**: `server/routes.ts` (lines 665-725)
**Issue**: Backtrack detection logic exists but time calculation still returns 0
**Fix Required**: Debug why minimum time thresholds aren't applied

### 3. OCR to Coordinates Pipeline
**Missing**: Direct integration between OCR output and Google Places resolution
**Fix Required**: Enhanced address resolution before route calculation

## Performance Issues
- **Processing Time**: 12+ seconds per recommendation
- **API Calls**: 4+ Google Maps calls per recommendation (expensive)
- **User Experience**: Too slow for real-world driving decisions

## What MVP Needs (Priority Order)

### Priority 1: Fix Location Resolution
1. Integrate Google Places API with DoorDash map processor
2. Combine OCR restaurant names with nearby street references
3. Return specific coordinates for route calculation

### Priority 2: Fix Route Time Calculation
1. Debug why opposite-direction trips show 0 minutes
2. Ensure minimum realistic time estimates are applied
3. Test backtrack distance detection logic

### Priority 3: End-to-End Testing
1. Test with real screenshots from both platforms
2. Verify recommendations match real-world driving experience
3. Confirm processing time under 10 seconds

## Focus Group Testing Priorities

### Test Case 1: Location Resolution
- Upload DoorDash screenshot with "Little Caesars"
- Verify system identifies specific restaurant location
- Check if coordinates are accurate for routing

### Test Case 2: Opposite Direction Detection
- Upload north-bound current trip
- Upload south-bound new offer
- Verify system shows realistic added time (30+ minutes)

### Test Case 3: Real-World Accuracy
- Test 5-10 actual driver scenarios
- Compare app recommendations to driver's real experience
- Measure processing speed

## Blockers to MVP Launch

### Technical Blockers
1. **Google Places integration not working** - Core functionality broken
2. **Zero minutes bug** - Produces wrong recommendations
3. **Processing speed** - Too slow for real-time decisions

### User Experience Blockers
1. **Upload workflow unclear** - Users don't understand two-screenshot process
2. **Error handling poor** - System fails silently when APIs break
3. **Mobile optimization incomplete** - Not optimized for in-car use

## Realistic MVP Timeline
- **If focus group identifies clear fixes**: 2-3 days implementation
- **If fundamental architecture issues**: 1-2 weeks rebuild
- **Current trajectory without changes**: Never reaches MVP quality

## Success Metrics for MVP
1. **Accuracy**: 80%+ of recommendations match driver's real experience
2. **Speed**: Under 10 seconds from upload to recommendation
3. **Reliability**: Works with 90%+ of screenshot uploads
4. **Usability**: Driver can use while stopped at red light

## Bottom Line
The system architecture is sound but two critical integration points are broken. Fix the Google Places integration and route calculation logic, and this becomes a functional MVP. Without these fixes, it remains a prototype that doesn't work reliably.