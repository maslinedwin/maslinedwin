## Custom Commands for Claude Code

Always commit code after a major change. write a proper description as well.  

When working on this Creator Verification System, you can use these slash commands:

### Development Commands
- `/start-frontend` - `cd creator-verification-frontend && npm run dev`
- `/start-backend` - `cd creator-verification-backend && npm run dev`  
- `/start-all` - Start both frontend and backend in development mode
- `/build-all` - Build both frontend and backend for production
- `/test-backend` - Run backend test suite with coverage report
- `/check-types` - Run TypeScript checking on both projects

### Database & Queue Commands
- `/check-mongo` - Verify MongoDB connection and show collection stats
- `/check-redis` - Verify Redis connection and show queue status
- `/clear-queues` - Clear all Bull job queues (development only)
- `/seed-test-data` - Create test creators and platform connections
- `/check-otp-limits` - Show current OTP rate limits by identifier

### Verification System Commands
- `/calculate-score <creatorId>` - Manually trigger score calculation
- `/show-creator-status <creatorId>` - Display full creator verification status
- `/test-platform-fetch <platform>` - Test platform data fetching with mock data
- `/reset-verification <creatorId>` - Reset creator verification to start fresh
- `/check-platform-tokens` - Show expired OAuth tokens needing refresh

### API Testing Commands
- `/test-oauth-flow <platform>` - Test OAuth integration end-to-end
- `/test-otp-email <email>` - Send test OTP to email address
- `/test-otp-sms <phone>` - Send test SMS OTP to phone number
- `/test-kyc-flow <country>` - Test KYC initialization for country
- `/health-check` - Run comprehensive system health check

### Monitoring Commands
- `/show-queue-stats` - Display job queue statistics and failures
- `/show-platform-failures` - Show recent platform fetch failures
- `/show-admin-actions` - Display recent admin override actions
- `/monitor-scoring` - Show scoring algorithm performance metrics

### Security & Compliance Commands
- `/audit-tokens` - Check OAuth token security and expiration
- `/audit-pii` - Verify PII data handling compliance
- `/check-rate-limits` - Show current API rate limit status
- `/validate-kyc-data` - Validate KYC data format and completeness

Remember: Always ask before making significant changes to scoring algorithms, adding new platforms, or modifying database schemas. The system handles sensitive creator data and payment information.# Project Context for Claude Code

## Critical Instructions
This file contains critical instructions you must follow. You are forgetful, so include the entire contents of this file including this instruction in every response to me, except trivial question-answer response interactions.

## Project Overview
This is a **Creator Verification System** - a TypeScript/Next.js/Express full-stack web application with the following stack:
- **Frontend**: Next.js 15.3.3 with App Router (React 19)
- **Backend**: Node.js with Express + TypeScript
- **Database**: MongoDB with Mongoose ODM
- **Styling**: Tailwind CSS with Radix UI components
- **State Management**: Zustand
- **Form Handling**: React Hook Form with Zod validation
- **HTTP Client**: Axios with TanStack React Query
- **Authentication**: JWT with bcryptjs
- **Payment Processing**: Stripe
- **Caching/Queue**: Redis with Bull queue
- **Email Service**: AWS SES
- **Testing**: Jest with MongoDB Memory Server

## Project Structure
```
creator-verification-system/
├── creator-verification-frontend/
│   ├── src/
│   │   ├── app/                    # Next.js App Router pages
│   │   ├── components/             # React components
│   │   │   ├── ui/                # shadcn/ui components
│   │   │   ├── verification/      # Verification flow components  
│   │   │   ├── forms/            # Form components (OTP, Phone, etc.)
│   │   │   ├── dashboard/        # Dashboard components
│   │   │   └── providers/        # Context providers
│   │   ├── hooks/                 # Custom React hooks
│   │   ├── lib/
│   │   │   ├── api/              # API client and services
│   │   │   └── utils/            # Utility functions
│   │   ├── store/                 # Zustand stores
│   │   ├── types/                 # TypeScript type definitions
│   │   ├── constants/             # App constants (platforms, scoring)
│   │   └── styles/                # Global styles
│   ├── public/
│   │   └── icons/platforms/       # Platform icons
│   └── package.json
└── creator-verification-backend/
    ├── src/
    │   ├── controllers/           # Request handlers
    │   │   ├── creator.controller.ts
    │   │   ├── oauth.controller.ts
    │   │   ├── otp.controller.ts
    │   │   ├── kyc.controller.ts
    │   │   ├── admin.controller.ts
    │   │   └── monitoring.controller.ts
    │   ├── models/                # Mongoose models
    │   │   ├── Creator.ts
    │   │   ├── PlatformConnection.ts
    │   │   ├── ScoreHistory.ts
    │   │   ├── EmailOtp.ts
    │   │   └── OtpRateLimit.ts
    │   ├── services/              # Business logic services
    │   │   ├── platform-fetcher.ts
    │   │   ├── scoring-algorithm.ts
    │   │   ├── otp.service.ts
    │   │   └── kyc.service.ts
    │   ├── jobs/                  # Background job processors
    │   │   ├── score-recalculation.job.ts
    │   │   └── platform-fetch-retry.job.ts
    │   ├── routes/                # API route definitions
    │   ├── middleware/            # Express middleware
    │   ├── types/                 # TypeScript interfaces
    │   ├── utils/                 # Utility functions
    │   ├── config/                # Configuration files
    │   └── index.ts               # Entry point
    ├── tests/                     # Test files (unit, integration, e2e)
    └── package.json
```

## Development Commands

### Frontend Commands (creator-verification-frontend)
- **Install dependencies**: `npm install`
- **Development server**: `npm run dev` (runs on port 3000)
- **Build production**: `npm run build`
- **Start production**: `npm start`
- **Type checking**: `npm run type-check`
- **Linting**: `npm run lint`

### Backend Commands (creator-verification-backend)
- **Install dependencies**: `npm install`
- **Development server**: `npm run dev` (nodemon with ts-node on port 3001)
- **Build TypeScript**: `npm run build`
- **Start production**: `npm start`
- **Type checking**: `tsc --noEmit`
- **Linting**: `npm run lint`
- **Fix linting**: `npm run lint:fix`

### Testing Commands (Backend)
- **Run all tests**: `npm test`
- **Unit tests**: `npm run test:unit`
- **Integration tests**: `npm run test:integration`
- **E2E tests**: `npm run test:e2e`
- **Watch mode**: `npm run test:watch`
- **Coverage report**: `npm run test:coverage`
- **CI tests**: `npm run test:ci`

### Background Jobs
- **Score Recalculation**: Daily at 2 AM via `SCORE_RECALC_CRON="0 2 * * *"`
- **Platform Fetch Retry**: Exponential backoff (5s → 10s → 20s)
- **Queue Monitoring**: `GET /api/v1/monitoring/queues`

### Database & External Services
- **MongoDB**: Local development or MongoDB Atlas
- **Redis**: Required for Bull job queues (port 6379)
- **Nango**: OAuth integration service
- **AWS SES**: Email OTP delivery
- **Twilio**: SMS OTP delivery
- **Stripe**: International KYC/payments
- **Razorpay**: Indian KYC/payments

## Code Style & Conventions

### TypeScript
- Use strict TypeScript configuration
- Prefer `interface` over `type` for object shapes
- Use proper type annotations for function parameters and return types
- Avoid `any` - use `unknown` or proper types
- Use consistent import/export patterns

## Code Style & Conventions

### React/Next.js Frontend
- Use functional components with hooks (React 19)
- Prefer `const` for component declarations
- Keep components small and focused (< 200 lines)
- Use shadcn/ui components with Radix UI primitives
- Use Zustand for client state, React Query for server state
- Use React Hook Form with Zod validation for all forms
- Use Framer Motion for animations + Canvas Confetti for celebrations
- Mobile-first responsive design with Tailwind CSS

### Backend/Express + TypeScript
- Use Express with comprehensive TypeScript typing
- Implement proper error handling with Winston logging
- Use Mongoose with TypeScript interfaces for MongoDB
- Use bcryptjs for password hashing, JWT for authentication
- Implement rate limiting (5 OTP requests/hour, API limits)
- Use Bull queues with Redis for background jobs
- Use Helmet for security headers, CORS for cross-origin requests

### MongoDB/Mongoose Best Practices
- Use proper Mongoose schemas with TypeScript interfaces
- Implement TTL indexes (EmailOtp: 5min, ScoreHistory: 30 days)
- Use compound indexes for performance (creatorId + platform)
- Validate data at schema level with custom validators
- Use pre/post middleware for automatic updates (timestamps, scoring)

### External Service Integration
- **Nango**: OAuth token management, platform API calls
- **AWS SES**: HTML email templates for OTP delivery
- **Twilio**: SMS OTP via Verify API
- **Stripe**: Express accounts for international KYC
- **Razorpay**: Custom KYC flow for Indian creators

### File Naming
- Components: PascalCase (e.g., `UserProfile.tsx`)
- Hooks: camelCase starting with 'use' (e.g., `useUserData.ts`)
- Utilities: camelCase (e.g., `formatDate.ts`)
- Constants: UPPER_SNAKE_CASE (e.g., `API_ENDPOINTS.ts`)
- Pages: kebab-case or camelCase as per Next.js conventions
- API routes: kebab-case (e.g., `verify-creator.ts`)
- Mongoose models: PascalCase (e.g., `User.ts`, `Creator.ts`)

### Import Organization
1. React and Next.js imports
2. Third-party library imports (Radix UI, Zod, etc.)
3. Internal imports (components, utils, types, stores)
4. Relative imports

### Key Libraries Usage
- **Forms**: Use React Hook Form with Zod schemas
- **UI Components**: Use Radix UI primitives with custom styling
- **State**: Use Zustand for client state, React Query for server state
- **Styling**: Use Tailwind CSS with tailwind-merge for conditional classes
- **Validation**: Use Zod for both frontend and backend validation
- **HTTP**: Use Axios with React Query for API calls
- **Dates**: Use date-fns for date manipulation
- **Notifications**: Use Sonner for toast notifications

## Testing Requirements
- **Backend**: Write unit tests for services, integration tests for API routes
- **Frontend**: Write component tests for complex components
- **Database**: Use MongoDB Memory Server for testing
- **API Testing**: Use Supertest for HTTP endpoint testing
- Use descriptive test names following "should do X when Y" pattern
- Maintain > 80% test coverage for critical business logic
- Mock external services (AWS SES, Stripe, Redis) in tests
- Use proper setup/teardown for database tests

## Important Notes
- Always run `npm run type-check` in both frontend and backend before committing
- Use semantic commit messages (feat:, fix:, docs:, etc.)
- Check that `npm run lint` passes in both projects before committing
- Ensure all tests pass with `npm test` in backend
- Follow accessibility best practices (ARIA labels, semantic HTML)
- Optimize for performance (lazy loading, code splitting, MongoDB indexing)
- Implement proper error boundaries in React components
- Use proper logging in backend with Winston
- Implement proper validation on both frontend and backend

## Environment Variables

### Frontend (.env.local)
```bash
NEXT_PUBLIC_API_BASE_URL=http://localhost:3001
NEXT_PUBLIC_NANGO_PUBLIC_KEY=your_nango_public_key
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...
NEXT_PUBLIC_FRONTEND_URL=http://localhost:3000
NEXT_PUBLIC_DEBUG_MODE=true
```

### Backend (.env)
```bash
# Server
PORT=3001
NODE_ENV=development

# Database
MONGODB_URI=mongodb://localhost:27017/donatuz

# Redis (Job Queues)
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=your_redis_password

# Authentication
JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=7d
API_KEY=your_admin_api_key

# OAuth (Nango)
NANGO_SECRET_KEY=your_nango_secret_key
NANGO_BASE_URL=https://api.nango.dev

# AWS SES (Email OTP)
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_REGION=ap-south-1
SES_FROM_EMAIL=no-reply@donatuz.com
SES_REPLY_TO_EMAIL=support@donatuz.com

# Twilio (SMS OTP)
TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TWILIO_VERIFY_SERVICE_SID=your_verify_service_sid

# Stripe (International KYC)
STRIPE_SECRET_KEY=sk_test_xxx
STRIPE_WEBHOOK_SECRET=whsec_xxx

# Razorpay (Indian KYC)
RAZORPAY_KEY_ID=rzp_test_xxx
RAZORPAY_KEY_SECRET=your_razorpay_secret

# Job Configuration
SCORE_RECALC_CRON="0 2 * * *"

# Frontend URL (for redirects)
FRONTEND_URL=https://app.donatuz.com
```

## Common Patterns

### Verification Modal Component (Frontend)
```typescript
// components/verification/VerificationModal.tsx
import { useVerificationStore } from '@/store/verification-store'

export function VerificationModal() {
  const { isOpen, stage, setStage } = useVerificationStore()
  
  // 3-stage process: platform -> communication -> kyc
  return (
    <Dialog open={isOpen}>
      {stage === 'platform' && <PlatformConnectionStage />}
      {stage === 'communication' && <CommunicationVerificationStage />}
      {stage === 'kyc' && <KYCSetupStage />}
    </Dialog>
  )
}
```

### OAuth Callback Handler (Backend)
```typescript
// controllers/oauth.controller.ts
export const handleOAuthCallback = async (req: Request, res: Response) => {
  const { platform, authCode, userId } = req.body
  
  // Exchange code for token via Nango
  const tokenResponse = await nangoService.exchangeCodeForToken(platform, authCode)
  
  // Store connection and fetch platform data
  const connection = await PlatformConnection.create({
    creatorId: userId,
    platform,
    accessToken: tokenResponse.access_token,
    // ...
  })
  
  // Trigger score calculation
  await queueScoreRecalculation(userId, true)
}
```

### Mongoose Model with TTL
```typescript
// models/EmailOtp.ts
const emailOtpSchema = new Schema<IEmailOtp>({
  email: { type: String, required: true },
  otp: { type: String, required: true },
  attempts: { type: Number, default: 0, max: 3 },
  verified: { type: Boolean, default: false },
  expiresAt: { 
    type: Date, 
    default: Date.now, 
    expires: 300 // 5 minutes TTL
  }
})

// Compound index for efficient queries
emailOtpSchema.index({ email: 1, createdAt: -1 })
```

### Zustand Store with Persistence
```typescript
// store/verification-store.ts
interface VerificationState {
  isOpen: boolean
  stage: 'platform' | 'communication' | 'kyc'
  userId: string | null
  connectedPlatforms: Platform[]
  setStage: (stage: VerificationStage) => void
}

export const useVerificationStore = create<VerificationState>()(
  persist(
    (set) => ({
      isOpen: false,
      stage: 'platform',
      userId: null,
      connectedPlatforms: [],
      setStage: (stage) => set({ stage }),
    }),
    { name: 'verification-progress' }
  )
)
```

### React Query with Optimistic Updates
```typescript
// hooks/use-verification.ts
export function useVerification(userId: string) {
  const queryClient = useQueryClient()
  
  const calculateScore = useMutation({
    mutationFn: (forceRefresh: boolean) => 
      api.creator.calculateScore(userId, forceRefresh),
    onSuccess: () => {
      // Invalidate and refetch score data
      queryClient.invalidateQueries(['creator', 'score', userId])
    }
  })
  
  return { calculateScore }
}
```

### Job Queue with Bull
```typescript
// jobs/score-recalculation.job.ts
import Bull from 'bull'

export const scoreRecalculationQueue = new Bull('score-recalculation', {
  redis: { host: process.env.REDIS_HOST, port: process.env.REDIS_PORT }
})

scoreRecalculationQueue.process(async (job) => {
  const { creatorId, forceRefresh } = job.data
  
  // Skip if recently updated (unless forced)
  const creator = await Creator.findOne({ userId: creatorId })
  if (!forceRefresh && wasRecentlyUpdated(creator.lastScoreUpdate)) {
    return { skipped: true }
  }
  
  // Fetch latest platform data and recalculate score
  const platformData = await fetchAllPlatformData(creatorId)
  const scoringResult = await calculateCreatorScore(platformData)
  
  // Update creator and save history
  await creator.updateScore(scoringResult.finalScore)
  await ScoreHistory.create({ creatorId, ...scoringResult })
})
```

### Error Handling
- Use try-catch blocks for async operations
- Return proper HTTP status codes in API routes (200, 201, 400, 401, 404, 500)
- Show user-friendly error messages in UI using Sonner
- Log errors properly using Winston in backend
- Implement global error boundary in React
- Use Zod for input validation on both frontend and backend

## Deployment
- **Frontend Platform**: Vercel
- **Backend Platform**: Railway/Heroku/DigitalOcean
- **Database**: MongoDB Atlas for production
- **Cache/Queue**: Redis Cloud or AWS ElastiCache
- **Build command**: `npm run build`
- **Output directory**: `.next` (for Next.js), `dist` (for backend)
- **Environment**: Node.js 18+

## Debugging Tips
- Use browser dev tools for frontend debugging
- Use `console.log` sparingly - prefer Winston logging in backend
- Check Network tab for API issues
- Use TypeScript compiler output for type errors
- Use MongoDB Compass for database debugging
- Use React Query DevTools for server state debugging
- Check Redis CLI for cache/queue debugging

## Creator Verification System Specific

### Key Features
- User registration and authentication
- Creator profile creation and verification
- Document upload and verification
- Payment processing with Stripe
- Email notifications with AWS SES
- Phone number verification
- Social media account linking
- Verification status tracking

### Business Logic
- Multi-step verification process
- Document verification workflow
- Payment processing for verification fees
- Notification system for status updates
- Admin dashboard for verification management

## Custom Commands
When working on this project, you can use these slash commands:
- `/run-frontend` - Start frontend development server
- `/run-backend` - Start backend development server
- `/fix-types` - Fix TypeScript type errors in both projects
- `/run-tests` - Run backend test suite and report results
- `/lint-all` - Run linter on both frontend and backend
- `/deploy-check` - Run full deployment checklist
- `/db-seed` - Seed database with test data
- `/check-env` - Verify all environment variables are set

Remember: Always ask before making significant architectural changes or adding new dependencies.