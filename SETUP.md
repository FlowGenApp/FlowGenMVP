# Flowgen Setup Instructions

## Quick Start for Focus Group

### Option 1: Live Testing (Recommended)
**Access the live Replit environment** provided by the team for immediate testing with real screenshots.

### Option 2: Local Development Setup

#### Prerequisites
- Node.js 18 or higher
- PostgreSQL database (or Neon account)
- Google Cloud API access

#### Required API Keys
1. **Google Cloud Vision API Key**
   - Go to Google Cloud Console
   - Enable Cloud Vision API
   - Create API key
   
2. **Google Maps API Key**
   - Enable Google Maps Directions API
   - Enable Google Places API
   - Enable Google Maps Geocoding API

3. **Database URL**
   - PostgreSQL connection string
   - Neon serverless recommended for testing

#### Installation Steps

1. **Clone Repository**
```bash
git clone [repository-url]
cd flowgen
```

2. **Install Dependencies**
```bash
npm install
```

3. **Environment Setup**
Create `.env` file:
```
GOOGLE_CLOUD_VISION_API_KEY=your_vision_api_key
GOOGLE_MAPS_API_KEY=your_maps_api_key
VITE_GOOGLE_MAPS_API_KEY=your_maps_api_key
DATABASE_URL=your_postgresql_url
```

4. **Database Setup**
```bash
npm run db:push
```

5. **Start Development Server**
```bash
npm run dev
```

6. **Access Application**
- Frontend: http://localhost:5000
- Backend API: http://localhost:5000/api

## Testing with Real Screenshots

### Required Test Data
For focus group testing, prepare screenshots from:
- **Uber Eats**: Current trip and new offer screens
- **DoorDash**: Map view with pickup/dropoff locations

### Test Scenarios
1. **Franchise Resolution**: Upload "Little Caesars" screenshot
2. **Opposite Direction**: North-bound current + South-bound offer
3. **Same Direction**: Logical route sequence
4. **Speed Test**: Measure processing time

## API Configuration

### Google Cloud Vision API
```javascript
// Automatically configured via GOOGLE_CLOUD_VISION_API_KEY
```

### Google Maps APIs
```javascript
// Places API: Business search and geocoding
// Directions API: Route calculation
// Configured via GOOGLE_MAPS_API_KEY
```

### Database Schema
```bash
# Push current schema to database
npm run db:push

# Generate new migrations (if needed)
npm run db:generate
```

## Troubleshooting

### Common Issues

#### 1. API Key Errors
- Verify API keys are correct and active
- Check API quotas and billing in Google Cloud Console
- Ensure required APIs are enabled

#### 2. Database Connection
- Verify DATABASE_URL format
- Check database permissions
- Run `npm run db:push` to sync schema

#### 3. Processing Timeouts
- Check network connectivity to Google APIs
- Verify API quotas aren't exceeded
- Monitor server logs for specific errors

### Debug Mode
```bash
NODE_ENV=development npm run dev
```

### Logs Location
- Server logs: Console output
- Request tracking: DEBUG level logs
- Error logs: Centralized error handler

## Focus Group Workflow

### 1. Environment Access
- Use provided Replit environment OR
- Set up local development following steps above

### 2. Testing Process
- Follow `FOCUS_GROUP_TESTING_GUIDE.md`
- Document issues in GitHub Issues
- Test with real delivery app screenshots

### 3. Feedback Submission
- Create GitHub Issues for bugs
- Use provided testing scenarios
- Focus on MVP-blocking issues

## Development Commands

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Run database migrations
npm run db:push

# Generate new migrations
npm run db:generate

# Run tests (if available)
npm test
```

## Architecture Overview

### Tech Stack
- **Frontend**: React 18 + TypeScript + Vite
- **Backend**: Node.js + Express + TypeScript
- **Database**: PostgreSQL + Drizzle ORM
- **APIs**: Google Cloud Vision, Google Maps, Google Places

### Key Directories
```
server/          # Backend API and logic
client/src/      # Frontend React application
shared/          # Shared types and schema
```

For detailed architecture information, see `README.md` and `CURRENT_COMPLETE_CODEBASE.txt`.