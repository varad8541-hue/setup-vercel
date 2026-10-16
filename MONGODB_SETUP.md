# MongoDB Atlas IP Whitelist Setup

Your bot is running but MongoDB can't connect because your Pterodactyl server's IP is not whitelisted in MongoDB Atlas.

## Quick Fix (2 minutes)

### Step 1: Find Your Server's IP
When your Pterodactyl server tries to connect, check the logs. Look for this error:
```
Could not connect to any servers in your MongoDB Atlas cluster. 
One common reason is that you're trying to access the database from an IP that isn't whitelisted.
```

The IP you need is your **Pterodactyl server's outgoing IP** (or your hosting provider's IP).

**Quick ways to find it:**
- Ask your hosting provider for the server IP
- Look at your Pterodactyl panel's server info
- Run this on the Pterodactyl server: `curl -s https://api.ipify.org`

### Step 2: Add IP to MongoDB Atlas

1. Go to **https://cloud.mongodb.com**
2. Sign in to your account
3. Go to **Deployment** → **Network Access** (left sidebar)
4. Click **+ Add IP Address**
5. Enter your Pterodactyl server's IP
6. Click **Add Entry**
7. Wait 1-2 minutes for it to apply

### Step 3: Restart Your Bot
Stop and restart the bot in Pterodactyl. It should now connect to MongoDB successfully.

---

## Alternative: Allow All IPs (Less Secure)
If you don't know the IP:
1. Go to **Network Access** in MongoDB Atlas
2. Click **+ Add IP Address**
3. Enter `0.0.0.0/0` (this allows connections from ANY IP - use with caution!)
4. Click **Add Entry**

⚠️ **Warning:** Allowing all IPs (`0.0.0.0/0`) is less secure. Only use this if you understand the risks.

---

## Verify Connection
After adding the IP and restarting, check the bot logs:
- ✅ Should see: `[INFO] Connected to MongoDB database`
- ❌ If still failing: Wait 2-3 minutes and try again

---

## Need Help?
- Check MongoDB Atlas documentation: https://docs.atlas.mongodb.com/security-whitelist/
- Verify your MONGO_URI in `.env` is correct
- Make sure your MongoDB cluster is in "Atlas" (not Community tier)
