# Building Your GitHub Pages Portfolio

## What This Is
A testing ground for:
- API integrations and data fetching
- Cloudflare Workers interaction
- LLM/AI chat capabilities
- Real-time data display
- Dark theme UI experimentation

**Not a CV. Not a portfolio showcase. Just a place to test things.**

---

## Setup Instructions
### 1. Create the Repository
1. Go to https://github.com/new
2. Name it: `sleepysdevin.github.io`
3. **Make it PUBLIC** (required for GitHub Pages)
4. Click "Create repository"

### 2. Clone and Install
```bash
git clone https://github.com/sleepysdevin/sleepysdevin.github.io.git
cd sleepysdevin.github.io
npm install
```

### 3. Development
```bash
npm run dev # Opens http://localhost:5173
```

### 4. Build & Deploy
```bash
npm run build
git add -A
git commit -m "Deploy"
git push origin main
```

The GitHub Actions workflow will automatically build and deploy to `https://sleepysdevin.github.io`

---

## Project Structure Explained
### `/src/components`
- **BentoBox.jsx** - Dashboard grid layout with stats
- **ApiFetcher.jsx** - Test different public APIs with TanStack Query
- **LLMChat.jsx** - Chat interface (configure your own API key)
- **CloudflareWorker.jsx** - Send requests to your workers

### `/src/hooks`
- **useApi.js** - Wrapper around TanStack Query for API calls

### `/src/lib`
- **apiEndpoints.js** - Curated list of free, interesting APIs
   - No generic todo/weather only examples
   - Real data sources: SpaceX, Countries, Quotes, Random Users, etc.

---

## How to Use Each Section
### 1. Dashboard (BentoBox)
Shows what's available. Quick reference.

### 2. APIs Tab
Click through different APIs to test them:
- **GitHub Trending** - Explore trending repos
- **Random User** - Generate fake user profiles
- **Quotes API** - Fetch random quotes
- **SpaceX Rockets** - Get rocket data
- **Countries** - Country information
- **Weather** - Open Meteo free API
- **IP Info** - Get your IP details
- And more...

**Add Your Own:** Edit `src/lib/apiEndpoints.js` to add more APIs.

### 3. Chat Tab
Configure your LLM of choice:
**Options:**
- **OpenAI** - `gpt-3.5-turbo` or `gpt-4`
- **Anthropic Claude** - via API
- **Hugging Face** - free models via inference API
- **Local Ollama** - run LLMs locally
- **Groq** - fast inference API

**Setup:**
1. Get an API key from your chosen provider
2. Click "Settings" in the chat tab
3. Paste your API key
4. Start chatting

The code is templated for OpenAI, but you can modify `LLMChat.jsx` to support others.

### 4. Workers Tab
Configure your Cloudflare Worker:
**Why?**
- Proxy requests to bypass CORS issues
- Add authentication
- Rate limiting
- Request/response transformation

**Setup:**
1. Create a worker at https://workers.cloudflare.com
2. Deploy it
3. Paste the worker URL in the settings
4. Send JSON requests and see responses

**Example Worker:**
```javascript
export default {
  async fetch(request) {
    if (request.method === 'POST') {
      const data = await request.json()
      // Do something with data
      return new Response(JSON.stringify({ success: true, data }))
    }
    return new Response('Worker is running')
  }
}
```

---

## Free APIs Worth Testing
Already included in `apiEndpoints.js`:
| API            | What It Does         | Use Case               |
|----------------|-----------------------|------------------------|
| GitHub         | Repo trending         | Discover projects      |
| SpaceX         | Rocket/mission data   | Space info             |
| Countries      | Country details       | Geography data         |
| Random User    | Fake profiles         | User data testing      |
| Quotes         | Random quotes         | Inspiration            |
| IP Geolocation | IP info               | Location detection     |
| Open Meteo     | Weather               | Real-time conditions   |
| Advice Slip    | Random advice         | Just for fun           |
| Useless Facts   | Random facts          | Just for fun           |
| Agify          | Age prediction        | Name analysis          |

**More to explore:**
- https://public-apis.io - Massive list of free APIs
- https://github.com/public-apis/public-apis - Curated list

---

## Customization Guide
### Change the Dark Theme
Edit `:root` in `src/App.css`:
```css
:root {
  --bg-primary: #0a0a0a; /* Main background */
  --bg-secondary: #1a1a1a; /* Secondary background */
  --accent: #7c3aed; /* Purple accent - change this */
  --text-primary: #ffffff; /* Main text */
}
```

### Add More Bento Boxes
Edit `src/components/BentoBox.jsx`:
```jsx
<div className="bento-item">
  <h3>Your Section</h3>
  <p>Content here</p>
</div>
```

Classes:
- `bento-item` - Standard box
- `bento-item large` - Full width
- `bento-item tall` - Double height

### Add New API
1. Edit `src/lib/apiEndpoints.js`
2. Add to `API_ENDPOINTS` object:
```javascript
myapi: { name: 'My API Name', url: 'https://api.example.com/endpoint' }
```
That's it. It'll appear in the dropdown automatically.

---

## Deployment
### Initial Deployment
1. Make sure your repo is **public**
2. Push to main branch
3. GitHub Actions automatically builds and deploys
4. Check https://github.com/sleepysdevin/sleepysdevin.github.io/actions

### Ongoing Deployments
Every push to `main` triggers a deployment. The workflow file (`.github/workflows/deploy.yml`) handles:
- Installing dependencies
- Building with Vite
- Uploading to GitHub Pages
- Publishing to your domain

### Custom Domain
If you have a custom domain:
1. Add `CNAME` file to repo root with your domain
2. Configure DNS at your registrar
3. GitHub Pages will use it automatically

---

## Troubleshooting
### Site shows 404
- Is the repo named `sleepysdevin.github.io`?
- Is it PUBLIC?
- Did the Actions workflow complete successfully?
- Check Actions tab to see build logs

### CORS Errors on APIs
Some APIs block browser requests. Solutions:
1. Use a CORS proxy (not ideal)
2. Route through Cloudflare Worker
3. Pick APIs that allow CORS
Most included APIs allow CORS. If one doesn't, use the Worker tab to proxy it.

### LLM Chat Not Working
- Did you paste a valid API key?
- Is the endpoint correct for your provider?
- Check browser console for errors
- API keys are stored in localStorage (device only)

### Worker Not Responding
- Is the worker deployed and live?
- Did you paste the correct URL?
- Is CORS enabled on the worker?

---

## Next Steps & Ideas
### Enhancements
- [ ] Add authentication to worker proxy
- [ ] Cache API responses in IndexedDB
- [ ] Dark/light theme toggle
- [ ] Export chat history
- [ ] Data visualization for API results
- [ ] Custom hooks for specific APIs
- [ ] Real-time data with WebSockets

### Integrations
- [ ] GitHub API - show your repos
- [ ] Twitter API - display tweets
- [ ] Spotify API - show listening activity
- [ ] Stripe API - payment integration
- [ ] Database - Firebase, Supabase, etc.

### Testing
- [ ] Unit tests with Vitest
- [ ] E2E tests with Playwright
- [ ] Performance monitoring
- [ ] Error logging/tracking

### DevOps
- [ ] Environment variables for API keys
- [ ] Secrets management
- [ ] Analytics
- [ ] Rate limiting

---

## Performance Tips
1. **TanStack Query** - Already set up to cache queries
2. **Lazy Loading** - Import components only when needed
3. **Code Splitting** - Vite does this automatically
4. **API Rate Limiting** - Implement exponential backoff
5. **Cloudflare** - Use workers to cache responses

---

## Security Notes
⚠️ **Don't commit API keys!**
- Store them in localStorage (lost on clear)
- Use environment variables for sensitive keys
- Never expose backend secrets in frontend code
- Use Cloudflare Workers as a proxy for sensitive requests

---

## That's It
You now have a blank canvas to:
- Test APIs
- Experiment with UI
- Learn React/Vite/TanStack
- Build tools while you learn

No pressure to make it "perfect" or "impressive." Just test, iterate, break things, fix them, move on.