# Cloudflare Pages Setup for Reviews

## Setup Steps

### 1. Create KV Namespace
In your Cloudflare dashboard:
1. Go to Workers & Pages > KV
2. Click "Create a namespace"
3. Name it: `portfolio-reviews`
4. Copy the namespace ID

### 2. Bind KV to Your Pages Project
1. Go to Workers & Pages > Your project
2. Settings > Functions > KV namespace bindings
3. Add binding:
   - Variable name: `REVIEWS_KV`
   - KV namespace: Select `portfolio-reviews`

### 3. Deploy
```bash
# If using Wrangler CLI
npx wrangler pages deploy .

# Or connect your GitHub repo to Cloudflare Pages
# It will auto-deploy on push
```

### 4. Initialize Reviews (Optional)
Add some sample reviews to KV:
1. Go to KV namespace in dashboard
2. Add key: `reviews`
3. Value:
```json
[
  {
    "name": "Sarah Johnson",
    "message": "Absolutely stunning work! The attention to detail is incredible.",
    "rating": 5,
    "timestamp": 1710172800000,
    "approved": true
  }
]
```

## How It Works

- **GET /api/reviews** - Fetches all approved reviews
- **POST /api/reviews** - Submits new review (pending approval)
- Reviews with `approved: false` won't show on the site
- You manually approve by editing the KV value in dashboard

## Alternative: Keep Using reviews.json

If you prefer not to use KV, you can keep the simple `reviews.json` approach:
- Reviews load from static JSON file
- You manually edit the file to add new reviews
- Simpler but requires manual updates

The current code supports both approaches!
