# Deployment Guide - AI Assistant

This guide provides step-by-step instructions for deploying the AI Assistant application to various platforms.

## 🚀 Deployment Platforms

### Vercel (Recommended)

Vercel is the recommended platform for deploying Next.js applications due to its seamless integration and automatic optimizations.

#### Prerequisites
- GitHub account
- Vercel account (free tier available)
- All environment variables ready

#### Step-by-Step Deployment

1. **Prepare Your Repository**
   ```bash
   # Ensure your code is committed and pushed to GitHub
   git add .
   git commit -m "Ready for deployment"
   git push origin main
   ```

2. **Connect to Vercel**
   - Go to [vercel.com](https://vercel.com/)
   - Sign in with your GitHub account
   - Click "New Project"
   - Import your AI Assistant repository

3. **Configure Project Settings**
   - **Framework Preset**: Next.js (auto-detected)
   - **Root Directory**: `./` (default)
   - **Build Command**: `npm run build` (default)
   - **Output Directory**: `.next` (default)
   - **Install Command**: `npm install` (default)

4. **Set Environment Variables**
   In the Vercel dashboard, add these environment variables:
   
   ```env
   GEMINI_API_KEY=your_actual_gemini_api_key
   NEXTAUTH_URL=https://your-app-name.vercel.app
   NEXTAUTH_SECRET=your_generated_secret
   GOOGLE_CLIENT_ID=your_google_client_id
   GOOGLE_CLIENT_SECRET=your_google_client_secret
   MONGODB_URI=your_mongodb_connection_string
   NEXT_PUBLIC_APP_NAME=AI Assistant
   ```

5. **Update Google OAuth Settings**
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Navigate to your OAuth 2.0 credentials
   - Add your Vercel domain to authorized redirect URIs:
     ```
     https://your-app-name.vercel.app/api/auth/callback/google
     ```

6. **Deploy**
   - Click "Deploy" in Vercel
   - Wait for the build to complete
   - Your app will be live at `https://your-app-name.vercel.app`

#### Automatic Deployments
- Every push to your main branch will trigger a new deployment
- Preview deployments are created for pull requests
- Rollback to previous deployments is available in the Vercel dashboard

### Render

Render is another excellent platform for deploying full-stack applications.

#### Step-by-Step Deployment

1. **Create Render Account**
   - Go to [render.com](https://render.com/)
   - Sign up and connect your GitHub account

2. **Create Web Service**
   - Click "New +" → "Web Service"
   - Connect your GitHub repository
   - Choose your AI Assistant repository

3. **Configure Service**
   - **Name**: `ai-assistant` (or your preferred name)
   - **Environment**: `Node`
   - **Region**: Choose closest to your users
   - **Branch**: `main`
   - **Build Command**: `npm install && npm run build`
   - **Start Command**: `npm start`

4. **Set Environment Variables**
   Add the same environment variables as Vercel, but update the URL:
   ```env
   NEXTAUTH_URL=https://your-app-name.onrender.com
   ```

5. **Update OAuth Settings**
   Add your Render domain to Google OAuth redirect URIs:
   ```
   https://your-app-name.onrender.com/api/auth/callback/google
   ```

6. **Deploy**
   - Click "Create Web Service"
   - Wait for the build and deployment to complete

### Docker Deployment

For containerized deployments, you can use Docker.

#### Dockerfile

Create a `Dockerfile` in your project root:

```dockerfile
# Use the official Node.js runtime as the base image
FROM node:18-alpine

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy the rest of the application code
COPY . .

# Build the Next.js application
RUN npm run build

# Expose the port the app runs on
EXPOSE 3000

# Define the command to run the application
CMD ["npm", "start"]
```

#### Docker Compose

Create a `docker-compose.yml` file:

```yaml
version: '3.8'
services:
  ai-assistant:
    build: .
    ports:
      - "3000:3000"
    environment:
      - GEMINI_API_KEY=${GEMINI_API_KEY}
      - NEXTAUTH_URL=${NEXTAUTH_URL}
      - NEXTAUTH_SECRET=${NEXTAUTH_SECRET}
      - GOOGLE_CLIENT_ID=${GOOGLE_CLIENT_ID}
      - GOOGLE_CLIENT_SECRET=${GOOGLE_CLIENT_SECRET}
      - MONGODB_URI=${MONGODB_URI}
      - NEXT_PUBLIC_APP_NAME=AI Assistant
    env_file:
      - .env.local
```

#### Deploy with Docker

```bash
# Build the image
docker build -t ai-assistant .

# Run the container
docker run -p 3000:3000 --env-file .env.local ai-assistant

# Or use Docker Compose
docker-compose up -d
```

## 🔧 Environment Variables Setup

### Required Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `GEMINI_API_KEY` | Google Gemini AI API key | `AIzaSy...` |
| `NEXTAUTH_URL` | Your app's URL | `https://yourapp.vercel.app` |
| `NEXTAUTH_SECRET` | Random secret for NextAuth | `generated-secret-key` |
| `GOOGLE_CLIENT_ID` | Google OAuth client ID | `123456789.apps.googleusercontent.com` |
| `GOOGLE_CLIENT_SECRET` | Google OAuth client secret | `GOCSPX-...` |
| `MONGODB_URI` | MongoDB connection string | `mongodb+srv://...` |

### Optional Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `NEXT_PUBLIC_APP_NAME` | Application name | `AI Assistant` |

### Generating Secrets

```bash
# Generate NextAuth secret
openssl rand -base64 32

# Or use Node.js
node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"
```

## 🔒 Security Considerations

### Production Checklist

- [ ] All environment variables are set correctly
- [ ] Google OAuth redirect URIs include production domain
- [ ] MongoDB Atlas network access is configured
- [ ] NEXTAUTH_SECRET is a strong, random value
- [ ] API keys are not exposed in client-side code
- [ ] HTTPS is enabled (automatic on Vercel/Render)

### MongoDB Atlas Security

1. **Network Access**
   - For production: Add specific IP addresses
   - For development: Use `0.0.0.0/0` (less secure)

2. **Database User**
   - Create a dedicated user for the application
   - Use strong passwords
   - Grant only necessary permissions

3. **Connection String**
   - Keep the connection string secret
   - Use environment variables only
   - Never commit to version control

## 🚨 Troubleshooting

### Common Issues

#### Build Failures

**Issue**: Build fails with TypeScript errors
```bash
Solution: Fix TypeScript errors locally first
npm run build  # Test locally
```

**Issue**: Missing environment variables
```bash
Solution: Ensure all required variables are set
# Check your deployment platform's environment variables section
```

#### Authentication Issues

**Issue**: Google OAuth not working
```bash
Solution: Check redirect URIs
1. Verify NEXTAUTH_URL matches your domain
2. Add correct redirect URI to Google Cloud Console
3. Ensure GOOGLE_CLIENT_ID and GOOGLE_CLIENT_SECRET are correct
```

**Issue**: NextAuth session errors
```bash
Solution: Check NEXTAUTH_SECRET
1. Ensure NEXTAUTH_SECRET is set
2. Generate a new secret if needed
3. Restart the application
```

#### Database Connection Issues

**Issue**: MongoDB connection fails
```bash
Solution: Check connection string and network access
1. Verify MONGODB_URI is correct
2. Check MongoDB Atlas network access settings
3. Ensure database user has correct permissions
```

### Debug Mode

Enable debug mode for NextAuth:

```env
NEXTAUTH_DEBUG=true
```

This will provide detailed logs for authentication issues.

### Logs and Monitoring

#### Vercel
- View logs in the Vercel dashboard
- Real-time logs during deployment
- Function logs for API routes

#### Render
- View logs in the Render dashboard
- Build logs and runtime logs
- Health checks and monitoring

## 📊 Performance Optimization

### Build Optimization

1. **Bundle Analysis**
   ```bash
   npm install --save-dev @next/bundle-analyzer
   ```

2. **Image Optimization**
   - Use Next.js Image component
   - Optimize images before upload
   - Use appropriate formats (WebP, AVIF)

3. **Code Splitting**
   - Automatic with Next.js
   - Use dynamic imports for large components

### Database Optimization

1. **MongoDB Indexes**
   - Create indexes for frequently queried fields
   - Monitor query performance

2. **Connection Pooling**
   - Mongoose handles this automatically
   - Configure pool size if needed

## 🔄 CI/CD Pipeline

### GitHub Actions

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to Vercel

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      
      - name: Setup Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '18'
          
      - name: Install dependencies
        run: npm ci
        
      - name: Run tests
        run: npm test
        
      - name: Build application
        run: npm run build
        
      - name: Deploy to Vercel
        uses: vercel/action@v20
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.ORG_ID }}
          vercel-project-id: ${{ secrets.PROJECT_ID }}
```

## 📈 Monitoring and Analytics

### Vercel Analytics
- Enable Vercel Analytics in your dashboard
- Monitor page views, performance, and user behavior

### Error Tracking
Consider integrating error tracking services:
- Sentry
- LogRocket
- Bugsnag

### Performance Monitoring
- Vercel Speed Insights
- Google PageSpeed Insights
- Web Vitals monitoring

---

**Need help with deployment? Check the troubleshooting section or create an issue in the repository.**

