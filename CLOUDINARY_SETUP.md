# Cloudinary Setup Guide

## Overview
The Instagram Reels Downloader now includes Cloudinary integration to upload downloaded videos to the cloud instead of storing them locally.

## Setup Instructions

### 1. Get Cloudinary Credentials
1. Sign up for a free account at [Cloudinary](https://cloudinary.com/)
2. Go to your Dashboard
3. Copy your Cloud Name, API Key, and API Secret

### 2. Set Environment Variables
Create a `.env` file in the root directory with the following variables:

```env
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
PORT=5000
```

### 3. Install Dependencies
The Cloudinary package is already included in `package.json`. Run:
```bash
npm install
```

### 4. How It Works
- Videos are downloaded locally first
- Then uploaded to Cloudinary in the `instagram-reels` folder
- Local files are automatically cleaned up after successful upload
- If Cloudinary upload fails, the system falls back to local storage

### 5. API Response Format
The API now returns different response formats:

**Successful Cloudinary Upload:**
```json
{
  "success": true,
  "message": "Video downloaded and uploaded to cloud successfully",
  "filename": "instagram_reel_1234567890.mp4",
  "cloudinaryUrl": "https://res.cloudinary.com/your-cloud/video/upload/instagram-reels/instagram_reel_1234567890.mp4",
  "cloudinaryId": "instagram_reel_1234567890",
  "downloadUrl": "https://res.cloudinary.com/your-cloud/video/upload/instagram-reels/instagram_reel_1234567890.mp4"
}
```

**Fallback to Local Storage:**
```json
{
  "success": true,
  "message": "Video downloaded locally (cloud upload failed)",
  "filename": "instagram_reel_1234567890.mp4",
  "filePath": "/path/to/local/file",
  "downloadUrl": "/downloads/instagram_reel_1234567890.mp4",
  "uploadError": "Error message from Cloudinary"
}
```

### 6. Benefits
- **Cloud Storage**: Videos are stored in the cloud, not on your server
- **Automatic Cleanup**: Local files are removed after upload
- **Better Performance**: Cloudinary provides fast CDN delivery
- **Fallback Support**: If cloud upload fails, local storage is used
- **Scalability**: No local storage limitations

### 7. Cloudinary Settings
- **Folder**: Videos are stored in the `instagram-reels` folder
- **Resource Type**: Set to `video` for proper handling
- **Overwrite**: Enabled to handle duplicate filenames
- **Invalidate**: Enabled for CDN cache invalidation

### 8. Troubleshooting
- **Upload Errors**: Check your Cloudinary credentials
- **Network Issues**: Ensure stable internet connection
- **File Size**: Cloudinary has upload limits (100MB for free tier)
- **Rate Limits**: Cloudinary has API rate limits

### 9. Security Notes
- Never commit your `.env` file to version control
- Keep your Cloudinary API secret secure
- Consider using environment variables in production 