# Contributing to Flowgen Focus Group Review

## Purpose
This repository is specifically for focus group review and testing of the Flowgen MVP. The goal is to identify and fix critical issues preventing MVP launch.

## Focus Group Testing Process

### 1. Issue Identification
Use GitHub Issues to report problems with these labels:
- `critical` - Blocks MVP launch
- `bug` - Functional problems
- `performance` - Speed/optimization issues
- `ux` - User experience problems

### 2. Testing Methodology
Follow the systematic approach in `FOCUS_GROUP_TESTING_GUIDE.md`:
- Test location resolution with franchise restaurants
- Test opposite-direction trip scenarios
- Measure processing speed and accuracy
- Verify real-world usability

### 3. Code Review Focus Areas
**Priority 1 - Critical Fixes**:
- `server/doordash-map-processor.ts` - Google Places integration
- `server/routes.ts` (lines 665-725) - Route calculation logic
- `server/places-api.ts` - Address resolution service

**Priority 2 - User Experience**:
- `client/src/pages/home.tsx` - Upload workflow
- `client/src/components/recommendation-card.tsx` - Results display

### 4. Feedback Format
When creating issues, include:
```
**File**: path/to/file.ts
**Issue**: Description of problem
**Expected**: What should happen
**Actual**: What currently happens
**Test Case**: Steps to reproduce
**Impact**: How this affects MVP readiness
```

## Current Known Issues

### Critical Issues
1. **Google Places API Not Connected** - `server/doordash-map-processor.ts`
2. **Zero Minutes Bug** - `server/routes.ts` route calculation
3. **Processing Speed** - 12+ seconds (target: under 10)

### Testing Priorities
- Location resolution accuracy (franchise restaurants)
- Route time calculation accuracy
- Processing speed optimization
- Mobile/in-car usability

## Development Environment

### Setup
```bash
npm install
npm run db:push
npm run dev
```

### Environment Variables
```
GOOGLE_CLOUD_VISION_API_KEY=required
GOOGLE_MAPS_API_KEY=required
DATABASE_URL=required
```

### Testing
- Live environment available via Replit
- Use real delivery app screenshots for testing
- Focus on Chicago area delivery scenarios

## Success Criteria
- 80%+ accuracy on location identification
- 90%+ accuracy on time estimates
- Under 10 seconds processing time
- Reliable handling of both Uber Eats and DoorDash

## Questions?
- Create GitHub Issues for technical questions
- Reference `FOCUS_GROUP_TESTING_GUIDE.md` for testing methodology
- See `MVP_STATUS_ASSESSMENT.md` for current state analysis