# Complete Setup Guide

## Quick Start (5 minutes)

### 1. Install Dependencies
\`\`\`bash
npm install
\`\`\`

### 2. Set Environment Variables
Create `.env.local`:
\`\`\`env
OPENAI_API_KEY=sk-...
\`\`\`

### 3. Run Development Server
\`\`\`bash
npm run dev
\`\`\`

### 4. Open Browser
Visit `http://localhost:3000`

### 5. Test Voice Commands
- Click "Start Listening"
- Say: "Add an expense of 50 for groceries"
- See the expense appear in the list

---

## Detailed Setup

### Option A: Using In-Memory Storage (No Database)

Perfect for testing and development without database setup.

**Steps:**
1. Install dependencies: `npm install`
2. Set `OPENAI_API_KEY` in `.env.local`
3. Run: `npm run dev`
4. Expenses are stored in memory (lost on server restart)

### Option B: Using PostgreSQL (Neon)

**Steps:**

1. **Create Neon Database**
   - Go to [neon.tech](https://neon.tech)
   - Create a new project
   - Copy connection string

2. **Set Environment Variable**
   \`\`\`env
   DATABASE_URL=postgresql://user:password@host/dbname
   OPENAI_API_KEY=sk-...
   \`\`\`

3. **Initialize Database**
   \`\`\`bash
   psql $DATABASE_URL -f scripts/init-database.sql
   \`\`\`

4. **Update API Routes**
   - Uncomment database code in `app/api/expenses/route.ts`
   - Import and use `query()` function from `lib/db.ts`

5. **Run Server**
   \`\`\`bash
   npm run dev
   \`\`\`

### Option C: Using MongoDB

**Steps:**

1. **Create MongoDB Database**
   - Go to [mongodb.com/cloud](https://mongodb.com/cloud)
   - Create a cluster
   - Get connection string

2. **Set Environment Variable**
   \`\`\`env
   MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/voice_app
   OPENAI_API_KEY=sk-...
   \`\`\`

3. **Update API Routes**
   - Uncomment MongoDB code in `app/api/expenses/route.ts`
   - Import and use `getExpensesCollection()` from `lib/mongodb.ts`

4. **Run Server**
   \`\`\`bash
   npm run dev
   \`\`\`

---

## Getting OpenAI API Key

1. Go to [platform.openai.com](https://platform.openai.com)
2. Sign up or log in
3. Navigate to API keys section
4. Create new secret key
5. Copy and paste into `.env.local`

**Cost:** ~$0.001 per command (very cheap for testing)

---

## Testing Voice Commands

### Test Cases

1. **Add Expense**
   - Say: "Add an expense of 50 for groceries"
   - Expected: Expense appears in list

2. **List Expenses**
   - Say: "Show all expenses"
   - Expected: Feedback shows expense count

3. **Delete Expense**
   - Say: "Delete expense 1"
   - Expected: First expense is removed

4. **Navigation**
   - Say: "Go to dashboard"
   - Expected: Navigate to dashboard page

5. **Help**
   - Say: "Help"
   - Expected: Help modal appears

### Troubleshooting Commands

If commands aren't working:

1. **Check Microphone Permission**
   - Browser should ask for microphone access
   - Allow access when prompted

2. **Check Console Errors**
   - Open DevTools (F12)
   - Check Console tab for errors
   - Check Network tab for API calls

3. **Test Regex Fallback**
   - Remove `OPENAI_API_KEY` from `.env.local`
   - Restart server
   - Try simple commands like "Add 50 for groceries"

---

## Deployment Checklist

- [ ] Set `OPENAI_API_KEY` in production environment
- [ ] Set `DATABASE_URL` if using database
- [ ] Run `npm run build` locally to test
- [ ] Deploy to Vercel/Railway/Heroku
- [ ] Test voice commands in production
- [ ] Monitor API usage and costs

---

## Common Issues & Solutions

### "Web Speech API not supported"
- Use Chrome, Edge, or Firefox
- Safari has limited support
- Check browser version

### "Command processing failed"
- Check OPENAI_API_KEY is valid
- Check API key has credits
- Check network connectivity
- Fallback regex parser should still work

### "Microphone not working"
- Check browser permissions
- Reload page and allow microphone
- Try different browser
- Check system microphone settings

### "Expenses not saving"
- If using in-memory: expenses reset on server restart
- If using database: check DATABASE_URL
- Check database connection
- Check API response in Network tab

---

## Next Steps

1. **Customize Categories**
   - Edit `ExpenseForm` component
   - Add your own expense categories

2. **Add Authentication**
   - Integrate Supabase Auth
   - Add user-specific expenses

3. **Add Analytics**
   - Create charts with Recharts
   - Show spending trends

4. **Deploy**
   - Push to GitHub
   - Connect to Vercel
   - Set environment variables
   - Deploy with one click

---

## Support

- Check README.md for more info
- Review code comments for implementation details
- Check browser console for error messages
- Test with simple commands first
