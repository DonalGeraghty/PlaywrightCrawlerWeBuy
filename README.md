# CEX Blu-Ray 4K Crawler

A Python-based web crawler that automatically monitors the CEX website for new 4K Blu-Ray releases and sends email notifications when new items become available.

## 🎯 What This Project Does

This crawler automatically:
1. **Scrapes** the CEX website for 4K Blu-Ray listings
2. **Tracks** daily changes in available inventory
3. **Identifies** newly added Blu-Ray titles
4. **Sends** email notifications with new releases and prices
5. **Maintains** a daily CSV database of all available items

## 🚀 How It Works

### Daily Workflow
1. **Crawl**: Visits the CEX Blu-Ray search page
2. **Filter**: Applies 4K and "In Stock Online" filters
3. **Scrape**: Collects all product titles and prices
4. **Compare**: Compares today's list with yesterday's list
5. **Generate**: Creates a diff of new Blu-Ray releases
6. **Notify**: Sends email with new items and prices
7. **Store**: Saves daily data to CSV files for future comparisons

### Data Storage
- **Daily CSV files**: Named with date (e.g., `2025-08-17.csv`)
- **Automatic cleanup**: Removes old CSV files, keeping only today's and yesterday's
- **Structured data**: Each CSV contains `id`, `name`, and `price` columns

## 🛠️ Prerequisites

- Python 3.8+
- Gmail account with App Password enabled
- Internet connection for web scraping

## 📦 Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd PlaywrightCrawlerWeBuy
   ```

2. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Install Playwright browsers**
   ```bash
   python -m playwright install
   ```

4. **Configure environment variables**
   Create a `.env` file in the project root:
   ```env
   RECIPIENT="your-email@gmail.com"
   SENDER="your-gmail@gmail.com"
   MY_KEY="your-gmail-app-password"
   ```

## 🔑 Gmail App Password Setup

To use Gmail for sending emails, you need to create an App Password:

1. Go to [Google Account Settings](https://myaccount.google.com/)
2. Navigate to **Security** → **2-Step Verification**
3. Scroll down to **App passwords**
4. Generate a new app password for "Mail"
5. Use this password in your `.env` file

## 🚀 Running the Project

### Option 1: Run the Test Suite (Recommended)
```bash
python -m pytest test_main.py -v
```

### Option 2: Run Individual Components
```bash
# Debug website structure
python debug_website.py

# Run specific test
python -m pytest test_main.py::test_we_buy -v
```

## 📁 Project Structure

```
PlaywrightCrawlerWeBuy/
├── test_main.py          # Main test file with crawler logic
├── cex_page.py          # CEX website interaction class
├── data_control.py      # Data processing and CSV management
├── my_mailer.py         # Email notification system
├── blu_ray.py           # BluRay data model
├── debug_website.py     # Website debugging utility
├── requirements.txt     # Python dependencies
├── .env                 # Environment configuration
└── README.md           # This file
```

## 🔧 Configuration

### Environment Variables
- `RECIPIENT`: Email address to receive notifications
- `SENDER`: Your Gmail address for sending emails
- `MY_KEY`: Gmail app password for authentication

### Customization Options
- **Browser**: Change `headless=False` to `True` for background operation
- **Filters**: Modify selectors in `cex_page.py` if website changes
- **Email content**: Customize email template in `my_mailer.py`

## 📊 Output Format

### CSV Structure
```csv
id,name,price
0,The Matrix 4K,€15.00
1,Blade Runner 4K,€12.50
2,Inception 4K,€18.00
```

### Email Notification
```
Subject: Your Item List

New Blu-Rays:

The Matrix 4K-€15.00
Blade Runner 4K-€12.50
Inception 4K-€18.00
```

## 🧪 Testing

The project uses pytest for testing. Key test features:
- **Browser automation**: Launches Chromium browser
- **Website interaction**: Clicks filters, accepts cookies
- **Data validation**: Ensures proper data extraction
- **Email testing**: Verifies notification system

## 🔍 Troubleshooting

### Common Issues

1. **Cookie acceptance fails**
   - Website structure may have changed
   - Run `debug_website.py` to inspect current elements
   - Update selectors in `cex_page.py`

2. **Email sending fails**
   - Verify Gmail app password is correct
   - Check `.env` file configuration
   - Ensure 2FA is enabled on Gmail account

3. **Playwright browser issues**
   - Run `python -m playwright install` to reinstall browsers
   - Check if antivirus is blocking browser downloads

### Debug Mode
Use the debug script to inspect website elements:
```bash
python debug_website.py
```

## 📈 Daily Usage

To run this crawler daily:

1. **Set up a cron job or task scheduler**
2. **Ensure your `.env` file is configured**
3. **Run the test suite**: `python -m pytest test_main.py`

The crawler will automatically:
- Generate today's CSV file
- Compare with yesterday's data
- Send email notifications for new items
- Clean up old CSV files

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## ⚠️ Disclaimer

This tool is for educational and personal use. Please respect the CEX website's terms of service and rate limiting. Consider adding delays between requests for production use.
