# AI Assistant - Powered by Gemini

A modern, minimalist AI assistant web application built with Next.js 14, featuring Google Authentication, MongoDB Atlas integration, and real-time chat functionality powered by Google's Gemini AI.

## ✨ Features

### 🔐 Authentication & Security
- **Google OAuth 2.0**: Secure sign-in with Google accounts
- **Session Management**: NextAuth.js for secure user sessions
- **Data Isolation**: Users can only access their own chat history
- **Environment Security**: All secrets stored in environment variables

### 🤖 AI-Powered Chat
- **Intelligent Conversations**: Powered by Google Gemini AI
- **Streaming Responses**: Real-time ChatGPT-like text streaming
- **File Upload Support**: Images, PDFs, and Word documents
- **Context Awareness**: AI remembers conversation context

### 💾 Persistent Data
- **MongoDB Atlas Integration**: Cloud database for chat storage
- **Real-time Saving**: Conversations saved automatically
- **Chat History**: Access all your past conversations
- **Cross-Device Sync**: Access your chats from any device

### 🎨 Modern UI/UX
- **Minimalist Design**: Clean blue and white color scheme
- **Responsive Layout**: Perfect on desktop and mobile
- **Smooth Animations**: Framer Motion for delightful interactions
- **Loading States**: Beautiful spinners and transitions
- **Chat Management**: Pin, organize, and search conversations

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm
- Google Cloud Console account (for OAuth)
- MongoDB Atlas account (for database)
- Google AI Studio account (for Gemini API)

### 1. Clone and Install

```bash
git clone <your-repository-url>
cd ai-assistant-app
npm install
```

### 2. Environment Setup

Create a `.env.local` file in the root directory:

```env
# Gemini AI API Configuration
GEMINI_API_KEY=your-gemini-api-key-here

# NextAuth Configuration
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-nextauth-secret-key-here

# Google OAuth Configuration
GOOGLE_CLIENT_ID=your-google-client-id-here
GOOGLE_CLIENT_SECRET=your-google-client-secret-here

# MongoDB Configuration
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/ai-assistant?retryWrites=true&w=majority

# Application Configuration
NEXT_PUBLIC_APP_NAME=AI Assistant
```

### 3. Run Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the application.

## 🔧 Detailed Setup Instructions

### Google Gemini API Setup

1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create a new API key
3. Copy the API key and add it to your `.env.local` file as `GEMINI_API_KEY`

### Google OAuth Setup

1. **Create a Google Cloud Project**:
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project or select an existing one

2. **Enable Google+ API**:
   - Navigate to "APIs & Services" > "Library"
   - Search for "Google+ API" and enable it

3. **Create OAuth 2.0 Credentials**:
   - Go to "APIs & Services" > "Credentials"
   - Click "Create Credentials" > "OAuth 2.0 Client IDs"
   - Choose "Web application"
   - Add authorized redirect URIs:
     - `http://localhost:3000/api/auth/callback/google` (for development)
     - `https://your-domain.com/api/auth/callback/google` (for production)

4. **Configure Environment Variables**:
   - Copy the Client ID and Client Secret
   - Add them to your `.env.local` file

### MongoDB Atlas Setup

1. **Create a MongoDB Atlas Account**:
   - Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
   - Sign up for a free account

2. **Create a Cluster**:
   - Choose the free tier (M0)
   - Select your preferred region
   - Create the cluster

3. **Create a Database User**:
   - Go to "Database Access"
   - Add a new database user with read/write permissions
   - Remember the username and password

4. **Configure Network Access**:
   - Go to "Network Access"
   - Add IP address `0.0.0.0/0` (for development) or your specific IPs

5. **Get Connection String**:
   - Go to "Clusters" and click "Connect"
   - Choose "Connect your application"
   - Copy the connection string
   - Replace `<password>` with your database user password
   - Add it to your `.env.local` file as `MONGODB_URI`

### NextAuth Secret

Generate a secure secret for NextAuth:

```bash
openssl rand -base64 32
```

Add the generated secret to your `.env.local` file as `NEXTAUTH_SECRET`.

## 🛠️ Tech Stack

### Frontend
- **Next.js 14**: React framework with App Router
- **TypeScript**: Type-safe JavaScript
- **Tailwind CSS**: Utility-first CSS framework
- **Framer Motion**: Animation library
- **Lucide React**: Beautiful icons

### Backend & Database
- **Next.js API Routes**: Server-side API endpoints
- **NextAuth.js**: Authentication library
- **MongoDB Atlas**: Cloud database
- **Mongoose**: MongoDB object modeling

### AI & Services
- **Google Gemini API**: AI language model
- **Google OAuth 2.0**: Authentication provider
- **File Processing**: PDF and Word document support

## 📁 Project Structure

```
ai-assistant-app/
├── src/
│   ├── app/                    # Next.js 14 app directory
│   │   ├── api/               # API routes
│   │   │   ├── auth/          # NextAuth configuration
│   │   │   ├── chat/          # Chat API endpoints
│   │   │   ├── chats/         # Chat management
│   │   │   └── upload/        # File upload handling
│   │   ├── login/             # Login page
│   │   ├── globals.css        # Global styles
│   │   ├── layout.tsx         # Root layout
│   │   ├── page.tsx           # Home page
│   │   └── providers.tsx      # Context providers
│   ├── components/            # React components
│   │   ├── chat/              # Chat-related components
│   │   ├── layout/            # Layout components
│   │   └── ui/                # UI components
│   ├── lib/                   # Utility libraries
│   │   ├── mongodb.ts         # Database connection
│   │   └── localStorage.ts    # Local storage utilities
│   ├── models/                # MongoDB models
│   │   ├── User.ts            # User model
│   │   └── Chat.ts            # Chat model
│   └── types/                 # TypeScript type definitions
├── .env.local                 # Environment variables
├── package.json               # Dependencies
└── README.md                  # This file
```

## 🔒 Security Features

- **Secure Authentication**: Google OAuth 2.0 integration
- **Session Management**: NextAuth.js with secure session handling
- **Environment Variables**: All secrets stored in environment variables
- **API Protection**: User session validation on all API endpoints
- **Data Isolation**: Users can only access their own chat history
- **CORS Configuration**: Secure cross-origin request handling

## 🎨 UI/UX Features

- **Minimalist Design**: Clean blue and white color scheme
- **Responsive Layout**: Works perfectly on desktop and mobile
- **Smooth Animations**: Framer Motion for delightful interactions
- **Loading States**: Beautiful loading spinners and transitions
- **File Upload**: Drag-and-drop file upload with preview
- **Chat Management**: Pin, delete, and organize conversations
- **User Profile**: Display user avatar and sign-out functionality

## 🚀 Deployment

### Vercel Deployment (Recommended)

1. **Push to GitHub**:
   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

2. **Deploy to Vercel**:
   - Go to [Vercel](https://vercel.com/)
   - Import your GitHub repository
   - Add environment variables in Vercel dashboard
   - Deploy

3. **Update OAuth Redirect URIs**:
   - Add your Vercel domain to Google OAuth authorized redirect URIs
   - Update `NEXTAUTH_URL` to your production domain

### Render Deployment

1. **Create a Render Account**:
   - Go to [Render](https://render.com/)
   - Connect your GitHub account

2. **Create a Web Service**:
   - Choose "Web Service"
   - Connect your repository
   - Configure build and start commands:
     - Build Command: `npm run build`
     - Start Command: `npm start`

3. **Add Environment Variables**:
   - Add all environment variables from your `.env.local`
   - Update `NEXTAUTH_URL` to your Render domain

## 🧪 Testing

### Manual Testing Checklist

#### Authentication
- [ ] Login page loads correctly
- [ ] Google sign-in button works
- [ ] User is redirected after successful login
- [ ] User profile displays correctly
- [ ] Sign-out functionality works

#### Chat Functionality
- [ ] Chat interface loads for authenticated users
- [ ] Messages send and receive properly
- [ ] Streaming responses display correctly
- [ ] File upload works for all supported formats
- [ ] Chat history saves to database
- [ ] Past chats load correctly

#### UI/UX
- [ ] Responsive design works on mobile
- [ ] Animations and transitions are smooth
- [ ] Loading states display properly
- [ ] Error handling shows appropriate messages
- [ ] Pin/unpin functionality works

### Performance Testing

- **First Contentful Paint**: < 1.5s
- **Largest Contentful Paint**: < 2.5s
- **Time to Interactive**: < 3.5s
- **Cumulative Layout Shift**: < 0.1

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

If you encounter any issues:

1. Check the [Issues](https://github.com/your-username/ai-assistant-app/issues) page
2. Create a new issue with detailed information
3. Include error messages and steps to reproduce

## 🙏 Acknowledgments

- [Google Gemini AI](https://ai.google.dev/) for the powerful AI capabilities
- [NextAuth.js](https://next-auth.js.org/) for authentication
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) for database hosting
- [Vercel](https://vercel.com/) for deployment platform
- [Next.js](https://nextjs.org/) for the amazing framework
- [Tailwind CSS](https://tailwindcss.com/) for styling
- [Framer Motion](https://www.framer.com/motion/) for animations

## 🔄 Version History

### Version 2.0.0 (Current)
- ✅ Google OAuth 2.0 authentication
- ✅ MongoDB Atlas integration
- ✅ Persistent chat history
- ✅ User session management
- ✅ Enhanced UI/UX with animations
- ✅ Mobile responsiveness improvements

### Version 1.0.0
- ✅ Basic chat interface with Gemini AI
- ✅ File upload and processing
- ✅ Local storage for chat history
- ✅ Responsive design

---

**Built with ❤️ using Next.js 14, Google Gemini AI, and MongoDB Atlas**

