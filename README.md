# Flowgen - Delivery Route Optimizer MVP

## Focus Group Review Repository

This repository contains the complete Flowgen codebase for focus group review and testing. The system helps gig delivery drivers make real-time accept/decline decisions on new offers while currently on active trips.

## 🚨 Current Status: NOT MVP READY

### Critical Issues Identified
1. **Location Resolution Broken** - Google Places API integration exists but isn't connected to DoorDash processor
2. **Route Calculation Bug** - Shows 0 minutes added time for opposite-direction trips
3. **Performance Issues** - Processing takes 12+ seconds (target: under 10 seconds)

## Quick Start for Focus Group

### 1. Access Live Application
- **Replit Environment**: Use provided Replit URL for live testing
- **Local Setup**: Clone this repository and follow setup instructions below

### 2. Critical Test Scenarios
- **Test 1**: Upload DoorDash screenshot with "Little Caesars" → Verify specific address resolution
- **Test 2**: Test opposite direction trips → Should show 30+ minutes, not 0 minutes
- **Test 3**: Measure processing speed → Should be under 10 seconds

### 3. Review Documentation
- `MVP_STATUS_ASSESSMENT.md` - Current state analysis
- `FOCUS_GROUP_TESTING_GUIDE.md` - Systematic testing methodology
- `CURRENT_COMPLETE_CODEBASE.txt` - File structure overview

## System Architecture

### User Flow
```
1. Driver uploads current trip screenshot (Uber Eats/DoorDash)
2. Driver uploads new offer screenshot
3. System calculates optimal route combining both deliveries
4. System provides accept/decline recommendation with time analysis
```

### Technical Flow
```
Screenshot → OCR (Google Vision) → Address Resolution (Google Places) → 
Route Calculation (Google Maps) → Time Comparison → Recommendation
```

### API Dependencies
- **Google Cloud Vision API** - OCR text extraction
- **Google Places API** - Business name to address resolution (BROKEN)
- **Google Maps Directions API** - Route calculation and time estimation
- **PostgreSQL** - Data storage

## Setup Instructions

### Prerequisites
```bash
Node.js 18+
PostgreSQL database
Google Cloud API keys
```

### Environment Variables Required
```
GOOGLE_CLOUD_VISION_API_KEY=your_vision_api_key
GOOGLE_MAPS_API_KEY=your_maps_api_key
DATABASE_URL=your_postgresql_url
```

### Installation
```bash
npm install
npm run db:push
npm run dev
```

## File Structure

### Critical Files for Review
- `server/routes.ts` - Main API logic with broken route calculation
- `server/doordash-map-processor.ts` - Location resolution (Google Places not integrated)
- `server/places-api.ts` - Google Places service (exists but unused)
- `client/src/pages/home.tsx` - Main user interface
- `client/src/components/recommendation-card.tsx` - Results display

### Database Schema
- `shared/schema.ts` - Data models for offers and decisions
- Uses Drizzle ORM with PostgreSQL

## Focus Group Feedback

### How to Provide Feedback
1. **GitHub Issues** - Create issues for specific bugs or improvements
2. **Direct Testing** - Use live Replit environment to test with real screenshots
3. **Code Review** - Review critical files listed above

### Testing Priorities
1. **Location Resolution** - Can system distinguish between 500+ Little Caesars locations?
2. **Route Accuracy** - Do time estimates match real driving experience?
3. **Processing Speed** - Is system fast enough for real-world use?

## Known Technical Debt

### Immediate Fixes Needed
1. **Connect Google Places API** to DoorDash processor (`server/doordash-map-processor.ts`)
2. **Fix route calculation logic** that returns 0 minutes (`server/routes.ts` lines 665-725)
3. **Optimize API call sequence** to reduce processing time

### Architecture Decisions
- Built with React/TypeScript frontend, Node.js/Express backend
- Uses PostgreSQL via Neon serverless
- Mobile-first design for in-car usage
- PWA capabilities for offline access

## Success Criteria for MVP
- 80% accuracy on location identification
- 90% accuracy on time estimates (within 10 minutes)
- Under 10 seconds processing time
- Handles both Uber Eats and DoorDash screenshots reliably

## Contact
- **Repository Issues** - Primary feedback method
- **Live Testing** - Use provided Replit environment
- **Documentation** - See focus group testing guide

---

**Bottom Line**: System architecture is sound, but two critical integration points are broken. Fix Google Places integration and route calculation logic to reach MVP status.