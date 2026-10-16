# Reborn Dashboard on Vercel

## Setup Steps

### 1. Push to GitHub
```bash
git add .
git commit -m "prepare dashboard for vercel"
git push
```

### 2. Create Vercel Project
- Go to https://vercel.com/new
- Import your GitHub repo
- Select the `dashboard` folder as the root directory

### 3. Environment Variables in Vercel
In Vercel project settings, add:
```
VITE_API_URL=https://your-pterodactyl-domain:25580
```

Replace `your-pterodactyl-domain:25580` with your actual bot server URL (where the API is running on port 25580).

### 4. Update Discord App Settings
In your Discord Developer Portal:
- Go to **OAuth2 > Redirects**
- Update **Redirect URI** to: `https://your-vercel-domain.vercel.app/login`
- Update **Authorized URLs** to include your Vercel domain

### 5. Restart Your Bot
Make sure your bot's API is still running (the `/api` endpoints):
```
npm run dev
```

## How It Works
- Dashboard runs on Vercel (fast CDN, worldwide)
- API calls go to your bot's API server (port 25580)
- CORS is enabled on the API to accept Vercel requests
- Environment variable controls the API URL

## Testing
1. Visit your Vercel dashboard URL
2. Click "Login with Discord"
3. Select your server
4. Dashboard should load with data from your bot

## Troubleshooting

### "API Connection Failed"
- Check that `VITE_API_URL` is set in Vercel
- Make sure your bot API is running
- Check browser console for exact error

### "Login redirects to blank page"
- Verify Discord app's Redirect URI matches Vercel URL
- Check that JWT tokens are being set in localStorage

### CORS Errors
- The API has CORS enabled, but check the error message
- May need to add your Vercel domain to Discord app settings
