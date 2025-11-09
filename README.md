# Farcaster Raffle Bot

A full-stack Farcaster raffle application with Frame integration, allowing users to join raffles directly through Farcaster Frames and admins to manage raffles through a beautiful web interface.

## Features

- 🎯 **Farcaster Frames Integration** - Users can join/leave raffles directly in Farcaster
- 🎨 **Beautiful Admin Panel** - Modern, responsive UI for managing raffles
- 🤖 **Anti-Bot Protection** - FID verification, rate limiting, and duplicate entry prevention
- ⏰ **Automatic Scheduler** - Auto-closes expired raffles and selects winners
- 📊 **Dashboard & Analytics** - Real-time stats and participant tracking
- 📥 **CSV Export** - Download participant lists for record keeping
- 🎲 **Fair Winner Selection** - Cryptographically random winner selection
- 🌓 **Dark/Light Mode** - Beautiful themes for both preferences

## Tech Stack

**Frontend:**
- React + TypeScript
- Wouter (routing)
- TanStack Query (data fetching)
- Shadcn UI + Tailwind CSS (styling)
- Lucide React (icons)

**Backend:**
- Node.js + Express
- Frog.js (Farcaster Frames)
- Neynar SDK (Farcaster API)
- node-cron (scheduler)
- In-memory storage (easily swappable to database)

**Security:**
- Helmet.js
- express-rate-limit
- FID verification via Neynar
- Duplicate entry prevention

## Prerequisites

- Node.js 20+
- Neynar API Key ([Get it here](https://neynar.com/))

## Installation

1. **Clone or open this project in Replit**

2. **Set up environment variables**

   Add your Neynar API key to Replit Secrets:
   - Key: `NEYNAR_API_KEY`
   - Value: Your API key from https://dev.neynar.com/

3. **Install dependencies** (auto-installed in Replit)
   ```bash
   npm install
   ```

4. **Start the application**
   ```bash
   npm run dev
   ```

   The app will be available at:
   - Admin Panel: `http://localhost:5000`
   - Frames: `http://localhost:5000/frame/{raffleId}`

## Usage

### Admin Panel

1. **Create a Raffle**
   - Navigate to "Create Raffle" in the sidebar
   - Fill in raffle details (title, description, prize, start/end times)
   - Click "Create Raffle"

2. **View & Manage Raffles**
   - Dashboard shows all active raffles and stats
   - Click "View Details" on any raffle to see participants
   - End raffles manually or let them auto-close at end time
   - Pick winners manually or let the scheduler auto-select

3. **Export Participants**
   - On any raffle detail page, click "Export CSV"
   - Downloads a CSV file with all participant information

### Farcaster Frames

1. **Share Frame URL**
   - Get the Frame URL from raffle details page
   - Share it in a Farcaster cast

2. **Users Can:**
   - View raffle details in the Frame
   - Click "Join Raffle" to participate
   - Click "Leave" to remove their entry
   - View winner when selected

## Automatic Features

### Scheduler (runs every minute)

- **Auto-Activate:** Pending raffles become active at start time
- **Auto-Close:** Active raffles close when end time is reached
- **Auto-Select Winner:** Randomly picks a winner from participants when raffle expires

## API Endpoints

### Raffles

- `GET /api/raffles` - List all raffles
- `GET /api/raffles/:id` - Get raffle with participants
- `POST /api/raffles` - Create new raffle
- `POST /api/raffles/:id/end` - End raffle manually
- `POST /api/raffles/:id/pick-winner` - Select winner manually
- `GET /api/raffles/:id/export` - Export participants as CSV

### Stats

- `GET /api/stats` - Get dashboard statistics

### Frames

- `GET /frame/:raffleId` - Main frame view
- `POST /frame/join/:raffleId` - Join raffle action
- `POST /frame/leave/:raffleId` - Leave raffle action
- `GET /frame/winner/:raffleId` - View winner

## Rate Limiting

- General API: 100 requests / 15 minutes per IP
- Raffle Creation: 10 raffles / hour per IP
- Frame Actions: 20 actions / minute per IP

## Testing on Warpcast

1. **Create a raffle** in the admin panel
2. **Copy the Frame URL** from the raffle details page
3. **Share it on Warpcast** (or use Frame validator at https://warpcast.com/~/developers/frames)
4. **Test joining/leaving** the raffle via Frame buttons
5. **Verify participants** appear in admin panel in real-time

## Security Features

- ✅ FID verification via Neynar SDK
- ✅ Duplicate entry prevention (one entry per FID per raffle)
- ✅ Rate limiting on all endpoints
- ✅ Helmet.js security headers
- ✅ Input validation with Zod schemas
- ✅ Protected admin routes

## Customization

### Using a Database

To switch from in-memory storage to a database:

1. Update `server/storage.ts` to implement `IStorage` with your DB
2. Keep the same interface methods
3. Update `storage` export to use your DB implementation

### Styling

- Colors: Edit `client/src/index.css` CSS variables
- Components: Modify Shadcn components in `client/src/components/ui`
- Layout: Update design in `design_guidelines.md`

## Project Structure

```
├── client/                 # Frontend React app
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   ├── pages/          # Page components
│   │   ├── lib/            # Utilities
│   │   └── App.tsx         # Main app with routing
├── server/                 # Backend Node.js app
│   ├── frame.ts            # Frog.js Frame handlers
│   ├── routes.ts           # Express API routes
│   ├── storage.ts          # Data storage interface
│   ├── scheduler.ts        # Cron job scheduler
│   └── index.ts            # Server entry point
├── shared/                 # Shared TypeScript types
│   └── schema.ts           # Data models and validation
└── README.md               # This file
```

## Troubleshooting

**Frames not loading:**
- Verify NEYNAR_API_KEY is set correctly
- Check that Frame URL is publicly accessible
- Test in Warpcast Frame validator first

**Winner not auto-selected:**
- Check server logs for scheduler errors
- Verify raffle has participants
- Ensure end time has passed

**Rate limit errors:**
- Wait for the time window to reset
- Adjust limits in `server/routes.ts` if needed for testing

## Future Enhancements

- [ ] PostgreSQL/SQLite persistence
- [ ] NFT/POAP minting for winners on Base
- [ ] Email notifications
- [ ] Multi-raffle campaigns
- [ ] Advanced analytics
- [ ] Webhook notifications
- [ ] Custom Frame images per raffle

## License

MIT

## Support

For issues or questions:
- Check the Replit console for error logs
- Verify all environment variables are set
- Review the Neynar API documentation: https://docs.neynar.com/

---

Built with ❤️ using Frog.js, Neynar SDK, and React
