# aadhritahack24
Hackathon batch submissions – Code &amp; PPT
# NotifyMe

An AI-powered sales opportunity detection system that automatically analyzes emails and SMS messages to identify and track business opportunities.

## Overview

NotifyMe helps sales teams capture every potential business opportunity by leveraging AI to analyze incoming communications. Using Claude AI, the system intelligently identifies opportunities, calculates confidence scores, suggests action items, and tracks them in a centralized dashboard.

### Key Features

- **AI-Powered Detection**: Uses Claude 3.5 Sonnet to analyze emails and SMS for business opportunities
- **Multi-Channel Support**: Integrates with Email and SMS through webhooks and Twilio
- **Confidence Scoring**: Automatically rates opportunities with confidence percentages
- **Dashboard Management**: Intuitive interface to view, filter, and manage opportunities
- **Action Item Tracking**: Suggested next steps for each opportunity
- **Notification System**: SMS and email notifications for new opportunities
- **MongoDB Backend**: Scalable NoSQL database for opportunity tracking
- **RESTful API**: Complete API for integrations and automation

## Tech Stack

### Frontend
- **Next.js 16** - React framework with App Router
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first styling
- **shadcn/ui** - Component library
- **SWR** - Data fetching and caching

### Backend
- **Flask** - Python web framework
- **MongoDB Atlas** - Cloud-hosted NoSQL database
- **Anthropic Claude** - AI-powered opportunity detection
- **Twilio** - SMS integration
- **Gmail API** - Email integration

## Quick Start

### Prerequisites

- Python 3.8+
- Node.js 16+
- MongoDB Atlas account (free tier available)
- Anthropic API key
- (Optional) Twilio and Gmail accounts

### 1. Clone and Setup

```bash
# Clone repository
git clone <your-repo>
cd notifyme

# Setup backend
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

# Setup frontend
cd ..
npm install
```

### 2. Configure Environment

**Backend** - Create `backend/.env`:
```env
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/notifyme
ANTHROPIC_API_KEY=sk-ant-xxxxxxxxxxxxx
FLASK_ENV=development
SECRET_KEY=your-dev-secret
FRONTEND_URL=http://localhost:3000
```

**Frontend** - Create `.env.local`:
```env
NEXT_PUBLIC_BACKEND_URL=http://localhost:5000
```

### 3. Start Development

**Terminal 1 - Backend:**
```bash
cd backend
python app.py
```

**Terminal 2 - Frontend:**
```bash
npm run dev
```

Visit `http://localhost:3000` to access the application.

## Documentation

- **[Setup Guide](./SETUP_GUIDE.md)** - Detailed setup instructions for all services
- **[API Reference](./API_REFERENCE.md)** - Complete API documentation
- **[Deployment Guide](./DEPLOYMENT.md)** - Production deployment instructions

## Core Endpoints

### Opportunities
- `GET /api/opportunities` - List opportunities
- `POST /api/opportunities` - Create opportunity
- `GET /api/opportunities/{id}` - Get opportunity details
- `PUT /api/opportunities/{id}` - Update opportunity
- `DELETE /api/opportunities/{id}` - Delete opportunity
- `GET /api/opportunities/stats` - Get statistics

### Analysis
- `POST /api/analysis/analyze` - Analyze message for opportunities
- `GET /api/analysis/suggest-response/{id}` - Get response suggestion
- `GET /api/analysis/logs/{id}` - Get analysis history

### Webhooks
- `POST /api/webhooks/email` - Handle email webhook
- `POST /api/webhooks/sms` - Handle SMS webhook

## Project Structure

```
notifyme/
├── app/                      # Next.js frontend
│   ├── dashboard/           # Dashboard pages
│   ├── layout.tsx           # Root layout
│   ├── page.tsx             # Home page
│   └── globals.css          # Global styles
├── backend/                 # Flask backend
│   ├── app.py              # Flask app factory
│   ├── config.py           # Configuration
│   ├── database.py         # MongoDB connection
│   ├── models.py           # Data models
│   ├── routes/             # API routes
│   ├── services/           # Business logic
│   ├── utils/              # Utility functions
│   └── requirements.txt    # Python dependencies
├── components/             # React components
├── lib/                    # Utility functions
├── public/                 # Static files
├── SETUP_GUIDE.md          # Setup instructions
├── API_REFERENCE.md        # API documentation
└── DEPLOYMENT.md           # Deployment guide
```

## Configuration

### MongoDB Atlas
- Create free tier cluster
- Get connection string
- Add to `MONGODB_URI` environment variable

### Anthropic Claude
- Sign up at console.anthropic.com
- Create API key
- Add to `ANTHROPIC_API_KEY` environment variable

### Twilio (Optional)
- Create account and get credentials
- Add to `TWILIO_ACCOUNT_SID`, `TWILIO_AUTH_TOKEN`, `TWILIO_PHONE_NUMBER`

### Gmail API (Optional)
- Create Google Cloud project
- Enable Gmail API
- Create OAuth credentials
- Save to `backend/credentials/gmail_credentials.json`

## Usage Examples

### Analyze an Email

```bash
curl -X POST http://localhost:5000/api/analysis/analyze \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Hi, we have a partnership opportunity that could benefit your business.",
    "sender": "partner@example.com",
    "message_type": "email",
    "user_id": "user123"
  }'
```

### Get Dashboard Statistics

```bash
curl http://localhost:5000/api/opportunities/stats?user_id=user123
```

### Update Opportunity Status

```bash
curl -X PUT http://localhost:5000/api/opportunities/66abc123def456789 \
  -H "Content-Type: application/json" \
  -d '{
    "status": "interested",
    "notes": "Following up next week"
  }'
```

## Development

### Running Tests

Backend:
```bash
cd backend
python -m pytest
```

Frontend:
```bash
npm run test
```

### Building for Production

Frontend:
```bash
npm run build
npm start
```

Backend:
```bash
gunicorn -w 4 -b 0.0.0.0:5000 app:create_app()
```

## Deployment

### Frontend
- Deploy to Vercel with one click
- See [Deployment Guide](./DEPLOYMENT.md) for details

### Backend
- Deploy to Railway, Heroku, or any Python-hosting service
- Set environment variables in production
- Configure MongoDB Atlas for production use

## Troubleshooting

### Connection Issues
- Verify MongoDB connection string and IP whitelist
- Check API keys are valid and not expired
- Ensure CORS is configured correctly

### Analysis Not Working
- Verify Anthropic API key is correct
- Check API usage and budget
- Review analysis logs for errors

### Webhooks Not Triggering
- Verify webhook URLs in service configurations
- Check firewall/network settings
- Review service logs for errors

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit changes: `git commit -m 'Add amazing feature'`
4. Push to branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## License

MIT License - see LICENSE file for details

## Support

For detailed setup instructions, see [Setup Guide](./SETUP_GUIDE.md)

For API documentation, see [API Reference](./API_REFERENCE.md)

For deployment, see [Deployment Guide](./DEPLOYMENT.md)

## NotifyMe Roadmap

- [ ] Advanced filtering and search
- [ ] Custom AI prompts per industry
- [ ] Team collaboration features
- [ ] Email integration with Gmail sync
- [ ] SMS integration with Twilio sync
- [ ] Analytics and reporting dashboard
- [ ] Mobile app
- [ ] API rate limiting and authentication
- [ ] Multi-language support

## Acknowledgments

- [Anthropic](https://www.anthropic.com/) - Claude AI
- [MongoDB](https://www.mongodb.com/) - Database
- [Twilio](https://www.twilio.com/) - SMS service
- [Vercel](https://vercel.com/) - Frontend hosting
- [shadcn/ui](https://ui.shadcn.com/) - Component library
