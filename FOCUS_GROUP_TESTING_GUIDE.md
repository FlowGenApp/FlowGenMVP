# Focus Group Testing Guide - Flowgen MVP

## Objective
Determine if Flowgen can reliably help drivers make accept/decline decisions on new offers within 10 seconds.

## Pre-Test Setup
1. Access Replit environment: [Your Replit URL]
2. Ensure Google API keys are configured
3. Have real Uber Eats/DoorDash screenshots ready for testing

## Critical Test Scenarios

### Test 1: Location Resolution (Most Critical)
**Goal**: Verify system can distinguish between franchise locations

**Steps**:
1. Upload DoorDash screenshot containing "Little Caesars" or similar chain
2. Check if system identifies specific restaurant address (not "Restaurant location")
3. Verify coordinates are accurate for that exact location

**Expected Result**: Specific address like "Little Caesars Pizza, 1224 N Clark St, Chicago, IL"
**Failure**: Shows "Restaurant location" or wrong franchise location

### Test 2: Opposite Direction Detection
**Goal**: Verify system catches backtrack scenarios

**Steps**:
1. Upload current trip going north (e.g., downtown to North Side)
2. Upload new offer going south (e.g., downtown to South Side)
3. Check added time estimate

**Expected Result**: 30-45 minutes added time
**Failure**: Shows 0 minutes or unrealistically low time

### Test 3: Same Direction Efficiency
**Goal**: Verify system recognizes efficient routes

**Steps**:
1. Upload current trip going north
2. Upload new offer continuing north (logical sequence)
3. Check added time estimate

**Expected Result**: 10-20 minutes added time
**Failure**: Shows excessive time or fails to calculate

### Test 4: Processing Speed
**Goal**: Measure real-world usability

**Steps**:
1. Time from screenshot upload to recommendation display
2. Test with various screenshot qualities
3. Test with both platforms (Uber Eats + DoorDash)

**Expected Result**: Under 10 seconds
**Failure**: Over 15 seconds consistently

### Test 5: Real Driver Scenarios
**Goal**: Test with actual driver decision points

**Use Real Screenshots**:
- Mix of efficient and inefficient offers
- Various restaurant types (chains vs local)
- Different distance ranges (2-8 miles)

**Validation**: Compare app recommendation to experienced driver's intuition

## What to Look For

### Signs of Success
- Specific restaurant addresses (not generic locations)
- Realistic time estimates that match driving experience
- Fast processing (under 10 seconds)
- Clear accept/decline recommendations

### Red Flags
- "Restaurant location" or "Customer location" instead of addresses
- 0 minutes added time for opposite directions
- Processing takes over 15 seconds
- System fails to process common screenshots

## Testing Methodology

### 1. Systematic Testing
- Test each scenario 3 times with different screenshots
- Document specific failures with screenshot examples
- Note any error messages or system timeouts

### 2. User Experience Testing
- Simulate in-car usage (quick decisions needed)
- Test with poor lighting/angled screenshots
- Verify mobile interface usability

### 3. Accuracy Validation
- For each recommendation, consider: "Would an experienced driver agree?"
- Compare estimated times to actual Google Maps routes
- Check if recommendations align with local knowledge

## Documentation Requirements

### For Each Test
**Record**:
- Screenshot used (save for reference)
- System response (exact addresses/times shown)
- Expected vs actual results
- Processing time
- Any errors or failures

### Overall Assessment
**Determine**:
- Is the core functionality working?
- Are recommendations reliable enough for real-world use?
- What are the biggest blockers to MVP launch?

## Focus Group Questions

### Technical Questions
1. Do the extracted addresses match what you see in screenshots?
2. Are time estimates realistic for Chicago driving?
3. Does the system handle franchise restaurants correctly?

### User Experience Questions
1. Is the upload process clear and fast enough?
2. Would you trust these recommendations while driving?
3. What information is missing or confusing?

### Business Viability Questions
1. Would this help you make better accept/decline decisions?
2. Is the processing speed acceptable for real-world use?
3. What would prevent you from using this app?

## Success Criteria for MVP
- 80% accuracy on location identification
- 90% accuracy on time estimates (within 10 minutes)
- Under 10 seconds processing time
- Handles both Uber Eats and DoorDash screenshots reliably

## Failure Indicators
- Cannot distinguish between franchise locations
- Consistently shows 0 minutes for opposite directions
- Takes over 15 seconds to process
- Fails on more than 20% of screenshot uploads

**Bottom Line**: If drivers wouldn't trust the recommendations enough to use while working, it's not MVP ready.