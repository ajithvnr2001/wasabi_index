# Wasabi S3 Index for Cloudflare Workers

A lightweight, serverless web interface to browse, preview, and download files from Wasabi S3 storage, powered by Cloudflare Workers.

## ✨ Features

- 📁 **Browse folders and files** with a clean, intuitive interface
- ⬇️ **Download files** with optimized streaming
- 👁️ **Preview** images, videos, PDFs, audio files, and text documents
- 🔐 **Optional password protection** using HTTP Basic Auth
- 🎨 **Dark/Light theme** support
- 📱 **Responsive design** - works on desktop and mobile
- 🚀 **Fast and efficient** - deployed on Cloudflare's global edge network
- 🔒 **AWS Signature V4** authentication for secure API requests
- 💰 **Cost-effective** - no egress fees with Wasabi

## 📋 Prerequisites

- Wasabi account ([Sign up here](https://wasabi.com))
- Cloudflare account with Workers enabled
- Basic knowledge of Cloudflare Workers deployment

## 🚀 Setup Instructions

### 1. Create Wasabi Account & Bucket

1. Sign up at [https://wasabi.com](https://wasabi.com)
2. Log in to Wasabi console
3. Navigate to **Buckets** → **Create Bucket**
4. Choose a **unique bucket name** (e.g., `my-storage-bucket`)
5. Select your preferred **region** (see supported regions below)
6. Click **Create Bucket**

### 2. Create IAM User & Access Keys

1. In Wasabi console, go to **Access Keys**
2. Click **Create Access Key**
3. Select **Programmatic (create S3 access key)**
4. Choose **Root User** or create a sub-user
5. Click **Create**
6. **Important**: Copy and save both:
   - Access Key ID
   - Secret Access Key
   
   ⚠️ The secret key is only shown once!

### 3. Deploy to Cloudflare Workers

1. Log in to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Go to **Workers & Pages** → **Create Application**
3. Click **Create Worker**
4. Give your worker a name (e.g., `wasabi-index`)
5. Click **Deploy**
6. Click **Edit Code**
7. **Copy the complete code** from `wasabi_index.js` (provided above)
8. **Paste** it into the worker editor, replacing all existing code
9. Click **Save and Deploy**

### 4. Configure Environment Variables

1. In your Worker dashboard, go to **Settings** → **Variables**
2. Under **Environment Variables**, add the following:

| Variable Name | Value | Example |
|---------------|-------|---------|
| `WASABI_ACCESS_KEY_ID` | Your Wasabi Access Key ID | `AKIAIOSFODNN7EXAMPLE` |
| `WASABI_SECRET_ACCESS_KEY` | Your Wasabi Secret Access Key | `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY` |
| `WASABI_BUCKET_NAME` | Your bucket name | `my-storage-bucket` |
| `WASABI_REGION` | Your bucket region | `us-east-1` |

3. Click **Save** for each variable
4. **Encrypt** the secret variables (recommended)

### 5. Test Your Deployment

1. Click on your worker's URL (e.g., `https://wasabi-index.yourname.workers.dev`)
2. You should see your bucket contents listed
3. Try clicking on folders and downloading files

## 🌍 Supported Regions

### North America
- `us-east-1` - US East (N. Virginia)
- `us-east-2` - US East (N. Virginia) - 2
- `us-west-1` - US West (Oregon)

### Europe
- `eu-central-1` - EU Central (Amsterdam)
- `eu-central-2` - EU Central (Frankfurt)
- `eu-west-1` - EU West (London)
- `eu-west-2` - EU West (Paris)

### Asia Pacific
- `ap-northeast-1` - Asia Pacific (Tokyo)
- `ap-northeast-2` - Asia Pacific (Osaka)
- `ap-southeast-1` - Asia Pacific (Singapore)
- `ap-southeast-2` - Asia Pacific (Sydney)

## ⚙️ Configuration Options

Edit the `CONFIG` object in the code to customize:

```javascript
const CONFIG = {
  siteName: "Wasabi S3 Index",    // Your site name
  siteIcon: "🪣",                  // Emoji or icon
  theme: "dark",                   // "dark" or "light"
  defaultPath: "",                 // Default folder path
  passwordProtected: false,        // Enable password protection
  password: "",                    // Set password if enabled
};
```

## 🔒 Optional: Enable Password Protection

1. In the worker code, locate the `CONFIG` object
2. Set `passwordProtected: true`
3. Set `password: "your-secure-password"`
4. Save and deploy

Users will need to enter the password using HTTP Basic Authentication.

## 📖 Usage

- **Browse folders**: Click on folder names to navigate
- **Download files**: Click the "Download" button next to any file
- **Preview files**: Click "Preview" for supported file types (images, PDFs, videos, audio)
- **Breadcrumb navigation**: Use the breadcrumb trail at the top to navigate back

## 🐛 Troubleshooting

### Error: "SignatureDoesNotMatch"
- Verify your Access Key ID and Secret Access Key are correct
- Ensure the region matches your bucket's region
- Check that all environment variables are properly set

### Error: "Missing required header"
- Make sure you're using the latest version of the code
- Verify the `x-amz-content-sha256` header is included

### Downloads are slow
- This is expected as files stream through Cloudflare Workers
- For better performance, consider using Cloudflare's CDN features
- The code includes caching headers for optimal performance

### Files not showing
- Check bucket permissions in Wasabi console
- Verify your IAM user has `s3:ListBucket` and `s3:GetObject` permissions
- Ensure the bucket name is spelled correctly

## 💡 Tips

- Keep your Secret Access Key **secure** - never commit it to public repositories
- Use Cloudflare's **Secrets** feature to encrypt sensitive environment variables
- Consider setting up **custom domains** for a professional appearance
- Enable **caching rules** in Cloudflare for faster repeat visits

## 🤝 Contributing

Contributions are welcome! Feel free to submit issues or pull requests.

## 📄 License

MIT License - feel free to use this project for personal or commercial purposes.

## 🙏 Credits

- Built for [Wasabi Hot Cloud Storage](https://wasabi.com)
- Powered by [Cloudflare Workers](https://workers.cloudflare.com)
- Inspired by Google Drive Index projects

***
