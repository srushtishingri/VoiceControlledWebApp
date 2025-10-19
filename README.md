# Voice-Controlled Expense Tracker

A full-stack web application that allows users to manage expenses using voice commands. Built with Next.js, React, Web Speech API, and AI-powered natural language processing.

## Features

- **Voice Command Recognition**: Use the Web Speech API to capture and process voice commands
- **Natural Language Processing**: AI-powered command parsing using OpenAI GPT
- **CRUD Operations**: Add, list, and delete expenses via voice or manual form
- **Real-time Feedback**: Visual and textual feedback for all actions
- **Navigation**: Voice-controlled navigation between pages
- **Responsive Design**: Works on desktop and mobile devices

## Tech Stack

### Frontend
- **Next.js 15** - React framework with App Router
- **React 19** - UI library
- **Web Speech API** - Browser-based speech recognition
- **Tailwind CSS** - Styling

### Backend
- **Next.js API Routes** - Serverless backend
- **AI SDK** - OpenAI integration for NLU
- **Node.js** - Runtime

### Database (Optional)
- **PostgreSQL** (via Neon) or **MongoDB**
- Connection utilities provided in `lib/db.ts` and `lib/mongodb.ts`

## Project Structure

\`\`\`
voice-app/
├── app/
│   ├── page.tsx                 # Main dashboard
│   ├── layout.tsx               # Root layout
│   ├── dashboard/page.tsx       # Dashboard page
│   ├── analytics/page.tsx       # Analytics page
│   ├── settings/page.tsx        # Settings page
│   └── api/
│       ├── expenses/
│       │   ├── route.ts         # GET/POST expenses
│       │   └── [id]/route.ts    # DELETE expense
│       └── process-command/
│           └── route.ts         # NLU command processing
├── components/
│   ├── voice-controller.tsx     # Voice input component
│   ├── expense-form.tsx         # Manual expense form
│   ├── expense-list.tsx         # Display expenses
│   └── command-help.tsx         # Help modal
├── lib/
│   ├── db.ts                    # PostgreSQL connection
│   ├── mongodb.ts               # MongoDB connection
│   └── ai-utils.ts              # AI utility functions
├── scripts/
│   └── init-database.sql        # Database schema
└── README.md
\`\`\`

## Installation & Setup

### Prerequisites
- Node.js 18+ and npm
- OpenAI API key (for AI-powered command parsing)
- (Optional) PostgreSQL or MongoDB database

### Step 1: Clone and Install Dependencies

\`\`\`bash
git clone <repository-url>
cd voice-app
npm install
\`\`\`

### Step 2: Environment Variables

Create a `.env.local` file in the root directory:

\`\`\`env
# OpenAI API Key (for AI-powered NLU)
OPENAI_API_KEY=your_openai_api_key_here

# Database (Optional - choose one)
# For PostgreSQL:
DATABASE_URL=postgresql://user:password@localhost:5432/voice_app

# For MongoDB:
MONGODB_URI=mongodb://localhost:27017/voice_app

# Development redirect URL for Supabase (if using Supabase auth)
NEXT_PUBLIC_DEV_SUPABASE_REDIRECT_URL=http://localhost:3000
\`\`\`

### Step 3: Database Setup (Optional)

If using PostgreSQL, run the initialization script:

\`\`\`bash
# Using psql
psql -U your_user -d voice_app -f scripts/init-database.sql

# Or use the Neon dashboard to run the SQL
\`\`\`

### Step 4: Run Development Server

\`\`\`bash
npm run dev
\`\`\`

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Usage

### Voice Commands

#### Expense Management
- **Add expense**: "Add an expense of 50 for groceries"
- **Add with description**: "Add 25 dollars for transportation yesterday"
- **List expenses**: "Show all expenses" or "List my expenses"
- **Delete expense**: "Delete expense 1"

#### Navigation
- **Go to dashboard**: "Go to dashboard" or "Navigate to dashboard"
- **Go to analytics**: "Show analytics" or "Open analytics"
- **Go to settings**: "Open settings"

#### General
- **Get help**: "Help" or "What can I say?"

### Manual Input

You can also add expenses using the form without voice:
1. Enter the amount
2. Select or type the category
3. Add an optional description
4. Click "Add Expense"

## API Endpoints

### Expenses

**GET /api/expenses**
- Retrieve all expenses
- Response: `[{ id, amount, category, description, date }]`

**POST /api/expenses**
- Create a new expense
- Body: `{ amount, category, description, date }`
- Response: `{ id, amount, category, description, date }`

**DELETE /api/expenses/[id]**
- Delete an expense by ID
- Response: `{ success: true }`

### Command Processing

**POST /api/process-command**
- Parse natural language command
- Body: `{ command: "string" }`
- Response: `{ action, data }`

## AI Command Parsing

The app uses OpenAI's GPT model to parse natural language commands. The AI extracts:
- **Action**: What the user wants to do (add_expense, list_expenses, delete_expense, navigate, help)
- **Data**: Structured information (amount, category, description, page)

### Fallback Regex Parser

If OpenAI API is not available, the app falls back to regex-based parsing for common commands.

## Deployment

### Deploy to Vercel

1. Push your code to GitHub
2. Connect your repository to Vercel
3. Add environment variables in Vercel dashboard
4. Deploy

\`\`\`bash
vercel deploy
\`\`\`

### Deploy to Other Platforms

The app can be deployed to any platform that supports Node.js:
- Heroku
- Railway
- Render
- AWS
- Google Cloud

## Browser Support

- Chrome/Edge 25+
- Firefox 25+
- Safari 14.1+
- Opera 27+

Note: Web Speech API support varies by browser. Check [caniuse.com](https://caniuse.com/speech-recognition) for current support.

## Troubleshooting

### Web Speech API Not Working
- Ensure you're using a supported browser
- Check browser permissions for microphone access
- Try using HTTPS (required for production)

### AI Commands Not Parsing
- Verify OPENAI_API_KEY is set correctly
- Check API key has sufficient credits
- The app will fall back to regex parsing if AI fails

### Database Connection Issues
- Verify DATABASE_URL is correct
- Ensure database server is running
- Check network connectivity

## Future Enhancements

- [ ] User authentication and multi-user support
- [ ] Expense categories and tags
- [ ] Budget tracking and alerts
- [ ] Data export (CSV, PDF)
- [ ] Mobile app with React Native
- [ ] Advanced analytics and charts
- [ ] Recurring expenses
- [ ] Receipt image recognition
- [ ] Multi-language support
- [ ] Offline mode with sync

## License

MIT

## Support

For issues or questions, please open an issue on GitHub or contact support.
