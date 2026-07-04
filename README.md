```markdown
# 🔥 BalanceHeat Hub - Ultimate Backend

**The world's most advanced "Mirror Economy" platform**  
A real-time peer-to-peer audio platform that connects strangers with opposite emotional states. Built with Node.js, Express, WebSockets, PostgreSQL, and Redis.

---

## 📋 Table of Contents

- [What This Does](#-what-this-does)
- [Core Philosophy](#-core-philosophy)
- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [Quick Start](#-quick-start-local-development)
- [API Endpoints](#-api-endpoints)
- [Database Schema](#-database-schema)
- [Admin Queries](#-admin-queries)
- [Deployment](#-deployment)
- [License](#-license)

---

## 🎯 What This Does

BalanceHeat Hub is not a chat app. It's a **psychological infrastructure** that:

- 🎤 Analyzes a 60-second voice sample to detect emotional state
- 🧠 Uses **AI-powered matching** to find your emotional opposite (not your clone)
- 📞 Connects you for a **7-minute anonymous audio call**
- ⏳ Forces a **5-minute cooldown** before rating (removes knee-jerk reactions)
- 💰 Rewards helpful users with **"Attentive Minutes"** (a currency for attention)
- 🔥 Tracks **"Heat" scores** (reputation that gives priority queueing)
- 👑 Awards **"Golden Earbud"** badges to top advisors (double minutes!)
- 🆘 Provides **"Emergency Mode"** for users in crisis (skip the queue)
- 📝 Has a **Reflection Journal** for private post-call notes
- 📊 Tracks **mood history** to show your emotional journey
- 🏆 Features a **Community Leaderboard** for top users
- 🔐 Includes **Phone Verification** for a safer community

---

## 🧠 Core Philosophy

> *"We don't match similarities. We match complementary suffering."*

When you're overwhelmed, you don't need someone who agrees with you. You need someone who can offer a completely different perspective. BalanceHeat Hub finds that person using emotional distance calculations.

---

## ✨ Key Features

### 1. Smart AI Matching
- Calculates emotional distance between users using Euclidean distance
- Matches you with your **emotional opposite** (not your clone)
- Uses topic filtering for better conversations

### 2. Golden Earbud Badge 👑
- Awarded to users with 5+ ratings averaging 4.5+
- **Double minutes** for every session
- Exclusive status symbol

### 3. Streak System
- **7-day streak:** 10 bonus minutes
- **30-day streak:** 30 bonus minutes
- **100-day streak:** 100 bonus minutes

### 4. Emergency Mode 🆘
- Skip the 90-second queue
- Immediate connection to an available user
- For genuine crisis situations

### 5. Mood Tracker
- Log your mood and energy level daily
- View your 30-day emotional history
- Track your progress over time

### 6. Reflection Journal
- Private post-call journal entries
- Only you can see them
- Save insights and lessons learned

### 7. Community Leaderboard
- Top 10 users by Heat score
- Competitive motivation
- Bragging rights

### 8. Phone Verification
- One-time SMS verification
- Reduces spam and trolls
- Safer community

### 9. Topics Filter
- Match based on shared interests
- Better conversation relevance

### 10. Transparency Stats
- Compare your rating against global averages
- See your progress

---

## 🛠️ Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Runtime** | Node.js (v20+) |
| **Framework** | Express.js |
| **Real-time** | WebSocket (ws library) |
| **Database** | PostgreSQL (users, balances, sessions, moods) |
| **Queue/Matching** | Redis (in-memory queue with smart matching) |
| **Auth** | None (fully anonymous + optional phone verification) |
| **Deployment** | Railway / Render / Fly.io |
| **Audio** | WebRTC (STUN/TURN) |

---

## 🚀 Quick Start (Local Development)

### Prerequisites
- Node.js v20+
- Docker (for PostgreSQL and Redis)
- npm or yarn

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/balanceheat-hub-backend.git
cd balanceheat-hub-backend
```

### 2. Install dependencies
```bash
npm install
```

### 3. Start PostgreSQL and Redis (using Docker)
```bash
docker run --name postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
docker run --name redis -p 6379:6379 -d redis
```

### 4. Set up environment variables
Create a `.env` file in the root directory:
```env
PORT=3000
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/postgres
REDIS_URL=redis://localhost:6379
TURN_SERVER_URL=stun:stun.l.google.com:19302
```

### 5. Start the server
```bash
node src/server.js
```

### 6. Test it
```bash
curl http://localhost:3000/health
# Should return: OK
```

### 7. Run with auto-restart (development)
```bash
npm run dev
```

---

## 📡 API Endpoints

### Health Check
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/health` | Check if server is running |

### User Management
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/calibrate` | Submit voice embedding & get matched |
| `GET` | `/api/balance` | Get balance, heat score, streak, stats |
| `GET` | `/api/match/status` | Check if user is matched |

### Call Management
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/call/end` | End a call session |
| `POST` | `/api/rating` | Submit rating after 5-min cooldown |

### Advanced Features
| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/mood/log` | Log mood and energy level |
| `GET` | `/api/mood/history` | Get 30-day mood history |
| `POST` | `/api/journal/save` | Save reflection journal entry |
| `GET` | `/api/journal/view` | View journal entries |
| `GET` | `/api/leaderboard` | Get top 10 users by Heat score |
| `POST` | `/api/verify/send` | Send phone verification code |
| `POST` | `/api/verify/confirm` | Confirm verification code |

---

## 📝 Example API Calls

### Calibrate (Start a session)
```json
POST /api/calibrate
{
  "anonymous_id": "user-abc-123",
  "embedding": [0.5, -0.2, 0.8, 0.1],
  "problem_category": "work_stress",
  "topics": ["career", "anxiety"],
  "is_emergency": false
}
```

**Response:**
```json
{
  "status": "matched",
  "session_id": "session-xyz-456",
  "turn_server": "stun:stun.l.google.com:19302"
}
```

### Get Balance & Stats
```json
GET /api/balance?anonymous_id=user-abc-123
```

**Response:**
```json
{
  "balance": 25.5,
  "heat_score": 78,
  "streak": 12,
  "is_golden_earbud": true,
  "stats": {
    "your_average": 4.2,
    "global_average": 3.8,
    "total_users": 156
  },
  "message": "👑 Golden Earbud! You earn double minutes!"
}
```

### End Call
```json
POST /api/call/end
{
  "session_id": "session-xyz-456",
  "anonymous_id": "user-abc-123",
  "ended_early": false
}
```

**Response:**
```json
{
  "status": "ended",
  "minutes_earned": 30,
  "streak": 12,
  "streak_bonus": 0
}
```

### Submit Rating
```json
POST /api/rating
{
  "session_id": "session-xyz-456",
  "anonymous_id": "user-abc-123",
  "helpfulness_score": 5,
  "acted_on_advice": true
}
```

**Response:**
```json
{
  "status": "rated"
}
```

### Log Mood
```json
POST /api/mood/log
{
  "anonymous_id": "user-abc-123",
  "mood": "calm",
  "energy_level": 8
}
```

### View Mood History
```json
GET /api/mood/history?anonymous_id=user-abc-123
```

**Response:**
```json
{
  "history": [
    { "mood": "calm", "energy_level": 8, "logged_at": "2026-07-02T10:00:00Z" },
    { "mood": "stressed", "energy_level": 3, "logged_at": "2026-07-01T10:00:00Z" }
  ]
}
```

### Save Journal Entry
```json
POST /api/journal/save
{
  "anonymous_id": "user-abc-123",
  "session_id": "session-xyz-456",
  "reflection": "Today I realized that I need to ask for help more often..."
}
```

### View Journal
```json
GET /api/journal/view?anonymous_id=user-abc-123
```

**Response:**
```json
{
  "journal": [
    {
      "session_id": "session-xyz-456",
      "reflection": "Today I realized...",
      "started_at": "2026-07-02T10:00:00Z"
    }
  ]
}
```

### Get Leaderboard
```json
GET /api/leaderboard
```

**Response:**
```json
{
  "leaderboard": [
    { "anonymous_id": "user-abc-123", "score": 95, "streak": 12, "is_golden_earbud": true },
    { "anonymous_id": "user-def-456", "score": 88, "streak": 8, "is_golden_earbud": false }
  ]
}
```

### Phone Verification
```json
POST /api/verify/send
{
  "phone_number": "+1234567890",
  "anonymous_id": "user-abc-123"
}
```

```json
POST /api/verify/confirm
{
  "anonymous_id": "user-abc-123",
  "code": 123456
}
```

---

## 🗄️ Database Schema

### `users`
| Column | Type | Description |
| :--- | :--- | :--- |
| `anonymous_id` | UUID (PK) | Anonymous user identifier |
| `created_at` | Timestamp | First use |
| `verified` | Boolean | Phone verification status |

### `balances` (Attention Currency)
| Column | Type | Description |
| :--- | :--- | :--- |
| `anonymous_id` | UUID (PK) | References users |
| `minutes` | Decimal | Current balance (starts at 10) |

### `heat` (Reputation)
| Column | Type | Description |
| :--- | :--- | :--- |
| `anonymous_id` | UUID (PK) | References users |
| `score` | Int (0-100) | Starts at 50 |
| `streak` | Int | Consecutive helpful ratings |
| `is_golden_earbud` | Boolean | Awarded to top advisors |
| `updated_at` | Timestamp | Last update |

### `sessions` (Call Records)
| Column | Type | Description |
| :--- | :--- | :--- |
| `session_id` | UUID (PK) | Unique call ID |
| `seeker_id` | UUID | Person seeking advice |
| `helper_id` | UUID | Person giving advice |
| `started_at` | Timestamp | Call start |
| `ended_at` | Timestamp | Call end |
| `ended_early` | Boolean | Triple-shake exit |
| `seeker_rating` | Int (1-5) | Rating given by seeker |
| `helper_rating` | Int (1-5) | Rating given by helper |
| `acted_on_advice` | Boolean | Did the seeker act? |
| `dispute_flag` | Boolean | Admin review needed |
| `reflection` | Text | Private journal entry |
| `is_emergency` | Boolean | Emergency mode flag |
| `topics` | Text[] | Conversation topics |

### `mood_logs`
| Column | Type | Description |
| :--- | :--- | :--- |
| `id` | Serial (PK) | Unique ID |
| `anonymous_id` | UUID | References users |
| `mood` | String | happy, sad, stressed, calm, etc. |
| `energy_level` | Int (1-10) | Energy rating |
| `logged_at` | Timestamp | When it was logged |

---

## 📊 Admin Queries

### Daily Health Check
```sql
-- Active users today
SELECT COUNT(DISTINCT anonymous_id) FROM sessions WHERE started_at > NOW() - INTERVAL '24 hours';

-- New users today
SELECT COUNT(*) FROM users WHERE created_at > NOW() - INTERVAL '24 hours';

-- Average balance
SELECT ROUND(AVG(minutes), 2) AS avg_balance FROM balances;
```

### Top Performers
```sql
-- Top 10 Heat leaders
SELECT anonymous_id, score, streak, is_golden_earbud FROM heat ORDER BY score DESC LIMIT 10;

-- Golden Earbud holders
SELECT COUNT(*) FROM heat WHERE is_golden_earbud = true;

-- Most active users
SELECT helper_id, COUNT(*) as sessions_helped FROM sessions GROUP BY helper_id ORDER BY sessions_helped DESC LIMIT 10;
```

### Quality Metrics
```sql
-- Average rating
SELECT ROUND(AVG(seeker_rating), 2) AS avg_rating FROM sessions WHERE seeker_rating IS NOT NULL;

-- Panic rate (early endings)
SELECT 
  COUNT(*) AS total_calls,
  SUM(CASE WHEN ended_early = true THEN 1 ELSE 0 END) AS panic_ends,
  ROUND(100.0 * SUM(CASE WHEN ended_early = true THEN 1 ELSE 0 END) / COUNT(*), 2) AS panic_percentage
FROM sessions WHERE started_at > NOW() - INTERVAL '7 days';

-- Emergency calls
SELECT COUNT(*) FROM sessions WHERE is_emergency = true AND started_at > NOW() - INTERVAL '7 days';
```

### Mood Analytics
```sql
-- Most common moods
SELECT mood, COUNT(*) FROM mood_logs GROUP BY mood ORDER BY COUNT(*) DESC;

-- Average energy by mood
SELECT mood, ROUND(AVG(energy_level), 2) AS avg_energy FROM mood_logs GROUP BY mood ORDER BY avg_energy DESC;
```

### Balance Economy
```sql
-- Check if users are running out of minutes
SELECT 
  COUNT(*) AS users_with_less_than_5_minutes 
FROM balances 
WHERE minutes < 5;

-- Users with no activity (stale)
SELECT b.anonymous_id, b.minutes 
FROM balances b 
LEFT JOIN sessions s ON b.anonymous_id = s.seeker_id 
WHERE s.session_id IS NULL;
```

---

## 🔐 Security & Privacy

- **Zero personal data**: No emails, no names, no phone numbers (unless you verify)
- **Audio processed on-device**: Voice embeddings never leave the user's phone
- **No recordings**: We never store call audio
- **Anonymous by design**: Users are identified only by UUIDs
- **Optional verification**: Phone verification is optional but recommended

---

## 🚀 Deployment

### Railway (Recommended)
1. Push code to GitHub
2. Go to [railway.app](https://railway.app)
3. Click "New Project" → "Deploy from GitHub repo"
4. Add PostgreSQL and Redis plugins (one click each)
5. Set `TURN_SERVER_URL` environment variable
6. Deploy!

### Render (Alternative)
1. Push code to GitHub
2. Go to [render.com](https://render.com)
3. Create a new Web Service connected to your repo
4. Add PostgreSQL and Redis manually

### Fly.io
```bash
fly launch
fly postgres create
fly redis create
fly deploy
```

---

## 🧪 Testing

### Manual Testing with cURL
```bash
# Start server
npm start

# Test health
curl http://localhost:3000/health

# Test calibration
curl -X POST http://localhost:3000/api/calibrate \
  -H "Content-Type: application/json" \
  -d '{"anonymous_id":"test-123","embedding":[0.5,0.3,-0.2],"problem_category":"general"}'

# Test balance
curl http://localhost:3000/api/balance?anonymous_id=test-123

# Test mood log
curl -X POST http://localhost:3000/api/mood/log \
  -H "Content-Type: application/json" \
  -d '{"anonymous_id":"test-123","mood":"happy","energy_level":8}'
```

### Automated Testing (Coming Soon)
Integration tests will be added in future versions.

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push: `git push origin feature/amazing-feature`
5. Open a Pull Request

---

## 📄 License

MIT License - Free for personal and commercial use.

---

## 🙏 Acknowledgments

- Built with ❤️ by the BalanceHeat Hub Team
- Powered by the open-source community

---

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/YOUR_USERNAME/balanceheat-hub-backend/issues)
- **Email**: your-email@example.com
- **Website**: [balanceheat.com](https://balanceheat.com)

---

**Built with ❤️ by the BalanceHeat Hub Team**

*"The mirror economy starts with a single echo."*
```

---# balanceheat-api
BalanceHeat Hub - Ultimate Mirror Economy Platform with 10 improvements
