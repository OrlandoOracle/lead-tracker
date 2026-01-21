# LookingGlass Lead Tracker

A web-based Kanban dashboard for insurance lead tracking with drag-and-drop functionality.

## Features

- **4 Kanban Columns**: 2ND CALL, GHOSTED, SOLD, CANT HELP
- **Drag & Drop**: Move leads between sections
- **Search**: Filter leads by name, phone, or notes
- **Auto-refresh**: Updates every 30 seconds
- **Mobile Responsive**: 4 columns on desktop, 2 on tablet, 1 on mobile
- **Dark Theme**: Modern, eye-friendly design
- **Click-to-call**: Phone numbers are clickable tel: links
- **Notes Preview**: Expandable notes on lead cards

## Setup

### 1. Configure Google Apps Script API

The dashboard requires a Google Apps Script web app that provides:

- `GET ?action=list` - Returns all leads organized by section
- `POST {action: "move", phone, section, notes}` - Moves a lead

### 2. Local Testing

Simply open `index.html` in your browser:

```bash
open ~/Desktop/LookingGlass/web/lead-tracker/index.html
```

On first load, you'll be prompted to enter the Google Apps Script URL.

### 3. Deployment Options

#### Option A: GitHub Pages (Free)

1. Create a new GitHub repository
2. Upload `index.html` to the repository
3. Go to Settings > Pages
4. Select "Deploy from a branch" and choose `main`
5. Your site will be available at `https://yourusername.github.io/repo-name/`

#### Option B: Render Static Site (Free)

1. Create a new Static Site on [Render](https://render.com)
2. Connect your GitHub repository
3. Set publish directory to `/` or the folder containing `index.html`
4. Deploy

#### Option C: Netlify (Free)

1. Drag and drop the folder to [Netlify Drop](https://app.netlify.com/drop)
2. Or connect a GitHub repository for automatic deploys

#### Option D: Simple HTTP Server

For local network access:

```bash
cd ~/Desktop/LookingGlass/web/lead-tracker
python3 -m http.server 8080
```

Then access at `http://localhost:8080` or `http://your-ip:8080`

## Configuration

### API URL

The Google Apps Script URL is stored in browser localStorage. To change it:

1. Click the **Settings** button in the header
2. Enter the new URL
3. Click **Save**

### Expected API Response Format

```json
{
  "success": true,
  "sections": [
    {
      "name": "2ND CALL",
      "color": "#fff299",
      "leads": [
        {
          "row": 28,
          "name": "Wendy Mcnabb",
          "agent": "S",
          "phone": "(281) 253-5694",
          "time": "11:00",
          "date": "1/7/2026",
          "firstNotes": "",
          "notes": ""
        }
      ]
    }
  ]
}
```

## Usage

### Moving Leads

1. Drag a lead card from one column
2. Drop it on the target column
3. Optionally add notes in the move dialog
4. The lead will be moved in the Google Sheet

### Searching

Type in the search box to filter leads by:
- Name
- Phone number
- Notes content

### Refreshing Data

- Data auto-refreshes every 30 seconds
- Click **Refresh** button for manual refresh
- Last updated timestamp shown in header

## Tech Stack

- React 18 (via CDN)
- Babel Standalone (JSX transformation)
- HTML5 Drag and Drop API
- CSS Grid for responsive layout
- LocalStorage for settings persistence

## Browser Support

- Chrome (recommended)
- Firefox
- Safari
- Edge

## Troubleshooting

### CORS Errors

If you see CORS errors, ensure your Google Apps Script is deployed with:
- Execute as: "Me"
- Who has access: "Anyone"

### API Not Responding

1. Check the Apps Script URL is correct
2. Verify the script is deployed (not just saved)
3. Check the Apps Script execution logs for errors

### Leads Not Moving

1. Check browser console for errors
2. Verify the phone number format matches the sheet
3. Check Apps Script logs for the move operation
