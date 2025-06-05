<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Colorado Red Rocks Adventure</title>
  
  <!-- Font Awesome for icons -->
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
    crossorigin="anonymous"
  />
  
  <style>
    :root {
      --primary-color: #8B4513;
      --secondary-color: #CD853F;
      --accent-color: #FF6B35;
      --mountain-blue: #4682B4;
      --forest-green: #228B22;
      --text-dark: #2c3e50;
      --text-light: #7f8c8d;
      --background-light: #f8f9fa;
      --card-background: #ffffff;
      --border-color: #e1e8ed;
      --success-color: #27ae60;
      --warning-color: #f39c12;
      --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      --shadow-hover: 0 8px 15px rgba(0, 0, 0, 0.15);
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #87CEEB 0%, #4682B4 50%, #8B4513 100%);
      min-height: 100vh;
      line-height: 1.6;
      color: var(--text-dark);
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 20px;
    }

    header {
      text-align: center;
      margin-bottom: 2rem;
      background: var(--card-background);
      padding: 2.5rem;
      border-radius: 20px;
      box-shadow: var(--shadow);
      position: relative;
      overflow: hidden;
    }

    header::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: linear-gradient(45deg, var(--mountain-blue), var(--primary-color));
      opacity: 0.05;
      z-index: 0;
    }

    header h1 {
      position: relative;
      z-index: 1;
      font-size: 2.8rem;
      background: linear-gradient(45deg, var(--primary-color), var(--mountain-blue));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 0.5rem;
      font-weight: 700;
    }

    .trip-dates {
      position: relative;
      z-index: 1;
      font-size: 1.2rem;
      color: var(--text-light);
      font-weight: 500;
    }

    .progress-indicator {
      position: fixed;
      top: 0;
      left: 0;
      height: 4px;
      background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
      z-index: 1000;
      transition: width 0.3s ease;
      width: 0%;
    }

    .day-card {
      background: var(--card-background);
      border-radius: 20px;
      margin-bottom: 2rem;
      box-shadow: var(--shadow);
      overflow: hidden;
      transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .day-card:hover {
      box-shadow: var(--shadow-hover);
      transform: translateY(-4px);
    }

    .day-header {
      background: linear-gradient(135deg, var(--primary-color), var(--mountain-blue));
      color: white;
      padding: 1.8rem;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: space-between;
      position: relative;
      overflow: hidden;
      transition: all 0.3s ease;
    }

    .day-header:hover {
      background: linear-gradient(135deg, #654321, #36648B);
    }

    .day-header::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
      transition: left 0.6s;
    }

    .day-header:hover::before {
      left: 100%;
    }

    .day-title {
      display: flex;
      align-items: center;
      gap: 1rem;
      font-size: 1.4rem;
      font-weight: 600;
    }

    .day-icon {
      font-size: 1.8rem;
      filter: drop-shadow(0 2px 4px rgba(0,0,0,0.3));
    }

    .expand-icon {
      font-size: 1.4rem;
      transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
      filter: drop-shadow(0 1px 2px rgba(0,0,0,0.3));
    }

    .day-card.expanded .expand-icon {
      transform: rotate(180deg);
    }

    .weather-banner {
      background: linear-gradient(135deg, var(--mountain-blue), #5F9EA0);
      color: white;
      padding: 1.2rem 1.8rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 1rem;
      position: relative;
      overflow: hidden;
    }

    .weather-banner::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="80" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="70" r="1.5" fill="rgba(255,255,255,0.1)"/></svg>');
      opacity: 0.3;
    }

    .weather-info {
      display: flex;
      align-items: center;
      gap: 1rem;
      position: relative;
      z-index: 1;
    }

    .weather-location {
      font-weight: 600;
      font-size: 1.1rem;
    }

    .weather-details {
      display: flex;
      gap: 2rem;
      flex-wrap: wrap;
      position: relative;
      z-index: 1;
    }

    .weather-item {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      font-size: 0.95rem;
      background: rgba(255,255,255,0.1);
      padding: 0.4rem 0.8rem;
      border-radius: 20px;
      backdrop-filter: blur(10px);
    }

    .day-content {
      display: none;
      padding: 2rem;
      background: linear-gradient(to bottom, #fafafa, #ffffff);
    }

    .day-card.expanded .day-content {
      display: block;
      animation: slideDown 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    }

    @keyframes slideDown {
      from {
        opacity: 0;
        transform: translateY(-20px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    .activity-list {
      list-style: none;
    }

    .activity-item {
      display: flex;
      align-items: flex-start;
      gap: 1.2rem;
      padding: 1.5rem;
      margin-bottom: 1rem;
      background: var(--card-background);
      border-radius: 15px;
      border-left: 5px solid var(--accent-color);
      box-shadow: 0 2px 8px rgba(0,0,0,0.08);
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      position: relative;
      overflow: hidden;
    }

    .activity-item::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: linear-gradient(135deg, rgba(255, 107, 53, 0.05), rgba(139, 69, 19, 0.05));
      opacity: 0;
      transition: opacity 0.3s ease;
    }

    .activity-item:hover::before {
      opacity: 1;
    }

    .activity-item:hover {
      transform: translateX(8px) translateY(-2px);
      box-shadow: 0 8px 25px rgba(0,0,0,0.15);
      border-left-color: var(--primary-color);
    }

    .activity-icon {
      color: var(--primary-color);
      font-size: 1.3rem;
      margin-top: 0.3rem;
      min-width: 24px;
      position: relative;
      z-index: 1;
    }

    .activity-content {
      flex: 1;
      position: relative;
      z-index: 1;
    }

    .activity-time {
      font-weight: 700;
      color: var(--secondary-color);
      margin-bottom: 0.5rem;
      font-size: 1.1rem;
    }

    .activity-description {
      color: var(--text-dark);
      margin-bottom: 0.8rem;
      line-height: 1.5;
    }

    .route-info {
      background: linear-gradient(135deg, #fff3cd, #ffeaa7);
      border: 1px solid #f6d55c;
      border-radius: 12px;
      padding: 1rem;
      margin: 0.8rem 0;
      font-style: italic;
      color: #856404;
      display: flex;
      align-items: flex-start;
      gap: 0.8rem;
      box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    }

    .route-info i {
      color: #d68910;
      margin-top: 0.2rem;
    }

    .button-group {
      display: flex;
      flex-wrap: wrap;
      gap: 0.8rem;
      margin-top: 1rem;
    }

    .link-button {
      display: inline-flex;
      align-items: center;
      gap: 0.6rem;
      padding: 0.7rem 1.2rem;
      background: var(--primary-color);
      color: white;
      text-decoration: none;
      border-radius: 25px;
      font-size: 0.9rem;
      font-weight: 500;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      box-shadow: 0 2px 8px rgba(139, 69, 19, 0.3);
      position: relative;
      overflow: hidden;
    }

    .link-button::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
      transition: left 0.5s;
    }

    .link-button:hover::before {
      left: 100%;
    }

    .link-button:hover {
      background: var(--secondary-color);
      transform: translateY(-2px);
      box-shadow: 0 4px 15px rgba(139, 69, 19, 0.4);
    }

    .mountain-button {
      background: var(--mountain-blue);
      box-shadow: 0 2px 8px rgba(70, 130, 180, 0.3);
    }

    .mountain-button:hover {
      background: #36648B;
      box-shadow: 0 4px 15px rgba(70, 130, 180, 0.4);
    }

    .weather-button {
      background: var(--forest-green);
      box-shadow: 0 2px 8px rgba(34, 139, 34, 0.3);
    }

    .weather-button:hover {
      background: #1F7A1F;
      box-shadow: 0 4px 15px rgba(34, 139, 34, 0.4);
    }

    .tips-section {
      background: var(--card-background);
      border-radius: 20px;
      padding: 2.5rem;
      box-shadow: var(--shadow);
      margin-top: 3rem;
      position: relative;
      overflow: hidden;
    }

    .tips-section::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: radial-gradient(circle at 20% 80%, rgba(255, 107, 53, 0.1) 0%, transparent 50%),
                  radial-gradient(circle at 80% 20%, rgba(139, 69, 19, 0.1) 0%, transparent 50%);
    }

    .tips-title {
      display: flex;
      align-items: center;
      gap: 1rem;
      font-size: 1.8rem;
      color: var(--text-dark);
      margin-bottom: 2rem;
      position: relative;
      z-index: 1;
      font-weight: 700;
    }

    .tips-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1.5rem;
      position: relative;
      z-index: 1;
    }

    .tip-item {
      display: flex;
      align-items: flex-start;
      gap: 1rem;
      padding: 1.5rem;
      background: linear-gradient(135deg, #ffffff, #f8f9fa);
      border-radius: 15px;
      border-left: 4px solid var(--warning-color);
      box-shadow: 0 4px 12px rgba(0,0,0,0.08);
      transition: all 0.3s ease;
    }

    .tip-item:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 20px rgba(0,0,0,0.12);
      border-left-color: var(--accent-color);
    }

    .tip-icon {
      color: var(--warning-color);
      font-size: 1.4rem;
      margin-top: 0.2rem;
    }

    .tip-text {
      color: var(--text-dark);
      line-height: 1.5;
      font-weight: 500;
    }

    .scroll-top {
      position: fixed;
      bottom: 2rem;
      right: 2rem;
      width: 50px;
      height: 50px;
      background: var(--primary-color);
      color: white;
      border: none;
      border-radius: 50%;
      font-size: 1.2rem;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      transition: all 0.3s ease;
      opacity: 0;
      transform: translateY(100px);
      z-index: 999;
    }

    .scroll-top.visible {
      opacity: 1;
      transform: translateY(0);
    }

    .scroll-top:hover {
      background: var(--secondary-color);
      transform: translateY(-3px);
      box-shadow: 0 6px 20px rgba(0,0,0,0.3);
    }

    @media (max-width: 768px) {
      .container {
        padding: 15px;
      }
      
      header {
        padding: 2rem;
      }
      
      header h1 {
        font-size: 2.2rem;
      }
      
      .day-title {
        font-size: 1.2rem;
      }
      
      .weather-details {
        gap: 1rem;
      }
      
      .weather-item {
        font-size: 0.85rem;
      }
      
      .activity-item {
        flex-direction: column;
        align-items: flex-start;
        gap: 0.8rem;
        padding: 1.2rem;
      }
      
      .tips-grid {
        grid-template-columns: 1fr;
      }
      
      .button-group {
        flex-direction: column;
        align-items: flex-start;
      }
      
      .link-button {
        align-self: flex-start;
      }
    }

    @media (max-width: 480px) {
      header h1 {
        font-size: 1.8rem;
        line-height: 1.2;
      }
      
      .trip-dates {
        font-size: 1rem;
      }
      
      .day-header {
        padding: 1rem;
      }
      
      .day-title {
        font-size: 1rem;
        line-height: 1.3;
      }
      
      .day-icon {
        font-size: 1.4rem;
      }
      
      .day-content {
        padding: 1rem;
      }
      
      .weather-banner {
        padding: 1rem;
        flex-direction: column;
        align-items: flex-start;
        gap: 0.8rem;
      }
      
      .weather-details {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 0.5rem;
        width: 100%;
      }
      
      .weather-item {
        font-size: 0.8rem;
        padding: 0.3rem 0.6rem;
      }
      
      .activity-item {
        padding: 1rem;
      }
      
      .activity-time {
        font-size: 1rem;
      }
      
      .route-info {
        padding: 0.8rem;
        font-size: 0.85rem;
      }
      
      .link-button {
        font-size: 0.85rem;
        padding: 0.6rem 1rem;
        width: 100%;
        justify-content: center;
      }
      
      .tips-title {
        font-size: 1.4rem;
      }
      
      .tip-item {
        padding: 1rem;
      }
      
      .scroll-top {
        width: 45px;
        height: 45px;
        bottom: 1rem;
        right: 1rem;
      }
    }

    @media print {
      body {
        background: white;
        font-size: 11pt;
        line-height: 1.4;
      }
      
      .container {
        max-width: none;
        padding: 0;
      }
      
      .day-card {
        box-shadow: none;
        border: 1px solid #ddd;
        break-inside: avoid;
        margin-bottom: 1rem;
      }
      
      .day-content {
        display: block !important;
      }
      
      .link-button, .scroll-top, .progress-indicator {
        display: none !important;
      }
      
      .weather-banner {
        background: #f0f0f0 !important;
        color: #333 !important;
      }
      
      .day-header {
        background: #e0e0e0 !important;
        color: #333 !important;
      }
      
      .activity-item {
        break-inside: avoid;
        margin-bottom: 0.5rem;
      }
      
      .tips-section {
        break-inside: avoid;
      }
      
      h1 {
        color: #333 !important;
      }
    }
  </style>
</head>
<body>
  <div class="progress-indicator" id="progressBar"></div>
  
  <div class="container">
    <header>
      <h1><i class="fa-solid fa-mountain"></i> Colorado Red Rocks Adventure</h1>
      <p class="trip-dates">June 6-8, 2025 • Rocky Mountain Adventure from the Heart of Texas</p>
    </header>

    <!-- Friday -->
    <div class="day-card" data-day="1">
      <div class="day-header" onclick="toggleDay(this)">
        <div class="day-title">
          <i class="fa-solid fa-plane-departure day-icon"></i>
          <span>Friday, June 6 – Travel Day: Fort Worth → Littleton, CO</span>
        </div>
        <i class="fa-solid fa-chevron-down expand-icon"></i>
      </div>
      <div class="weather-banner">
        <div class="weather-info">
          <i class="fa-solid fa-mountain" style="font-size: 1.8rem;"></i>
          <span class="weather-location">Littleton, CO</span>
        </div>
        <div class="weather-details">
          <div class="weather-item">
            <i class="fa-solid fa-thermometer-half"></i>
            <span>High: 78°F</span>
          </div>
          <div class="weather-item">
            <i class="fa-solid fa-moon"></i>
            <span>Low: 52°F</span>
          </div>
          <div class="weather-item">
            <i class="fa-solid fa-sun"></i>
            <span>Sunny</span>
          </div>
          <div class="weather-item">
            <i class="fa-solid fa-eye"></i>
            <span>Clear views</span>
          </div>
        </div>
        <a href="https://weather.com/weather/today/l/80127:4:US" target="_blank" class="link-button weather-button">
          <i class="fa-solid fa-external-link-alt"></i> Full Forecast
        </a>
      </div>
      <div class="day-content">
        <ul class="activity-list">
          <li class="activity-item">
            <i class="fa-solid fa-home activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">6:00-8:00 AM</div>
              <div class="activity-description">Final packing and departure preparation from <em>5509 Tuxbury Pond Dr, Fort Worth, TX</em></div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-route activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">8:00 AM - Departure</div>
              <div class="activity-description">Begin drive to Littleton, Colorado</div>
              <div class="route-info">
                <i class="fa-solid fa-route"></i>
                <span>Route (~650 miles, 9h 45m): I-35W N → I-35 N → I-25 N → C-470 W to Littleton</span>
              </div>
              <div class="button-group">
                <a href="https://www.google.com/maps/dir/5509+Tuxbury+Pond+Dr,+Fort+Worth,+TX/5669+S+Alkire+St,+Littleton,+CO+80127" target="_blank" class="link-button">
                  <i class="fa-solid fa-map"></i> View Full Route
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-gas-pump activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">11:30 AM - First Stop</div>
              <div class="activity-description">
                <strong>Amarillo, TX</strong> (3.5 hours from Fort Worth) - Fuel up, stretch, and grab snacks
                <br><em>Recommended: Love's Travel Stop or Buc-ee's for clean facilities and food</em></div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-utensils activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">2:00 PM - Lunch Break</div>
              <div class="activity-description">
                <strong>Colorado Springs, CO</strong> (7 hours from Fort Worth) - Lunch and final supply stop
                <br><em>1 hour remaining to destination - perfect timing for a meal break</em></div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-bed activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">6:00-7:00 PM - Arrival</div>
              <div class="activity-description">Check-in at <strong>La Quinta Inn & Suites by Wyndham Littleton/Red Rocks</strong><br>
              5669 S Alkire Street, Littleton, Colorado, 80127</div>
              <div class="button-group">
                <a href="https://www.wyndhamhotels.com/laquinta" target="_blank" class="link-button mountain-button">
                  <i class="fa-solid fa-hotel"></i> Hotel Website
                </a>
                <a href="tel:+13039729300" class="link-button">
                  <i class="fa-solid fa-phone"></i> Call Hotel
                </a>
                <a href="https://www.google.com/maps/place/5669+S+Alkire+St,+Littleton,+CO+80127" target="_blank" class="link-button">
                  <i class="fa-solid fa-map-marker-alt"></i> Hotel Location
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-utensils activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">7:30 PM</div>
              <div class="activity-description">Dinner at hotel restaurant or nearby options - Rest up for tomorrow's adventures!</div>
            </div>
          </li>
        </ul>
      </div>
    </div>

    <!-- Saturday -->
    <div class="day-card" data-day="2">
      <div class="day-header" onclick="toggleDay(this)">
        <div class="day-title">
          <i class="fa-solid fa-mountain-sun day-icon"></i>
          <span>Saturday, June 7 – Red Rocks & Denver Exploration</span>
        </div>
        <i class="fa-solid fa-chevron-down expand-icon"></i>
      </div>
      <div class="weather-banner">
        <div class="weather-info">
          <i class="fa-solid fa-sun" style="font-size: 1.8rem;"></i>
          <span class="weather-location">Red Rocks Area</span>
        </div>
        <div class="weather-details">
          <div class="weather-item">
            <i class="fa-solid fa-thermometer-half"></i>
            <span>High: 82°F</span>
          </div>
          <div class="weather-item">
            <i class="fa-solid fa-moon"></i>
            <span>Low: 55°F</span>
          </div>
          <div class="weather-item">
            <i class="fa-solid fa-sun"></i>
            <span>Perfect weather</span>
          </div>
          <div class="weather-item">
            <i class="fa-solid fa-wind"></i>
            <span>Light breeze</span>
          </div>
        </div>
        <a href="https://weather.com/weather/today/l/80465:4:US" target="_blank" class="link-button weather-button">
          <i class="fa-solid fa-external-link-alt"></i> Full Forecast
        </a>
      </div>
      <div class="day-content">
        <ul class="activity-list">
          <li class="activity-item">
            <i class="fa-solid fa-coffee activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">8:00 AM</div>
              <div class="activity-description">Hotel breakfast and preparation for the day</div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-mountain activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">9:30 AM</div>
              <div class="activity-description">Lookout Mountain Park & Buffalo Bill's Grave (20 minutes from hotel)</div>
              <div class="route-info">
                <i class="fa-solid fa-info-circle"></i>
                <span>Stunning panoramic views of Denver and the Front Range. Visit Buffalo Bill's grave and museum. Great photo opportunities!</span>
              </div>
              <div class="button-group">
                <a href="https://www.google.com/maps/dir/5669+S+Alkire+St,+Littleton,+CO+80127/Lookout+Mountain+Park,+Golden,+CO" target="_blank" class="link-button">
                  <i class="fa-solid fa-map"></i> Directions to Lookout Mountain
                </a>
                <a href="https://www.buffalobill.org/" target="_blank" class="link-button mountain-button">
                  <i class="fa-solid fa-external-link-alt"></i> Buffalo Bill Museum
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-hiking activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">11:00 AM</div>
              <div class="activity-description">Easy hiking at Lookout Mountain:
                <br><strong>• Nature Trail</strong> (0.8 miles, easy) - Gentle walk with interpretive signs
                <br><strong>• Windy Saddle Trail</strong> (1.2 miles, moderate) - Better views of Denver skyline
                <br><strong>• Picnic areas</strong> - Perfect for snacks with mountain views</div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-utensils activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">12:30 PM</div>
              <div class="activity-description">Lunch in Golden - Historic downtown with brewery options and mountain charm</div>
              <div class="button-group">
                <a href="https://www.google.com/maps/search/restaurants+golden+colorado" target="_blank" class="link-button">
                  <i class="fa-solid fa-utensils"></i> Golden Restaurants
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-mountain activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">2:30 PM</div>
              <div class="activity-description">Drive to Roxborough State Park (25 minutes from Golden)</div>
              <div class="route-info">
                <i class="fa-solid fa-route"></i>
                <span>Golden to Roxborough: US-6 W → C-470 W → N Rampart Range Rd → Roxborough Park Dr</span>
              </div>
              <div class="button-group">
                <a href="https://www.google.com/maps/dir/Golden,+CO/Roxborough+State+Park,+Littleton,+CO" target="_blank" class="link-button">
                  <i class="fa-solid fa-map"></i> Route to Roxborough
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-camera activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">3:00 PM</div>
              <div class="activity-description"><strong>🏔️ Roxborough State Park - Colorado's Hidden Gem! 🏔️</strong>
                <br>Dramatic red-rock formations similar to Garden of the Gods - National Natural Landmark with 4,000 acres of stunning scenery and wildlife viewing opportunities.</div>
              <div class="route-info">
                <i class="fa-solid fa-star"></i>
                <span>$10 entrance fee, no dogs allowed. Limited parking fills up fast on weekends!</span>
              </div>
              <div class="button-group">
                <a href="https://cpw.state.co.us/state-parks/roxborough-state-park" target="_blank" class="link-button mountain-button">
                  <i class="fa-solid fa-info"></i> Park Information
                </a>
                <a href="https://www.google.com/maps/place/Roxborough+State+Park" target="_blank" class="link-button">
                  <i class="fa-solid fa-map-marker-alt"></i> Park Location
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-hiking activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">3:30 PM</div>
              <div class="activity-description">Afternoon hiking at Roxborough:
                <br><strong>• Fountain Valley Loop</strong> (2.3 miles, moderate) - Winds through red rock formations
                <br><strong>• Willow Creek Trail</strong> (1.3 miles, easy) - Known for wildflowers and bird watching
                <br><strong>• South Rim Trail</strong> (0.9 miles, easy) - Great views with less crowds
                <br><strong>• Wildlife viewing</strong> - Mule deer, fox, golden eagles, and occasional bears</div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-camera-retro activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">4:30 PM</div>
              <div class="activity-description">Photography and exploration time - Perfect lighting for red rock photos as the afternoon sun hits the formations. Visit the historic Persse Place ruins from 1903.</div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-utensils activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">5:30 PM</div>
              <div class="activity-description">Return to Littleton area for early dinner before concert</div>
              <div class="route-info">
                <i class="fa-solid fa-clock"></i>
                <span>Roxborough to Red Rocks: 15 minutes via Roxborough Park Dr → Chatfield Ave → Morrison Rd</span>
              </div>
              <div class="button-group">
                <a href="https://www.google.com/maps/search/restaurants+littleton+colorado" target="_blank" class="link-button">
                  <i class="fa-solid fa-utensils"></i> Littleton Restaurants
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-route activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">6:30 PM</div>
              <div class="activity-description">Drive to Red Rocks for evening concert (15 minutes from Littleton)</div>
              <div class="route-info">
                <i class="fa-solid fa-clock"></i>
                <span>Perfect timing! Much shorter drive from Roxborough/Littleton area. Gates typically open 2 hours before show.</span>
              </div>
              <div class="button-group">
                <a href="https://www.google.com/maps/dir/Littleton,+CO/Red+Rocks+Park+and+Amphitheatre,+Morrison,+CO" target="_blank" class="link-button">
                  <i class="fa-solid fa-map"></i> Littleton to Red Rocks
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-music activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">8:00 PM</div>
              <div class="activity-description"><strong>🎸 CONCERT: Big Head Todd and the Monsters at Red Rocks Amphitheatre! 🎸</strong>
                <br>Experience live music at one of the world's most beautiful venues with stunning red rock formations as the backdrop. This iconic Colorado band is perfect for your Colorado adventure!</div>
              <div class="route-info">
                <i class="fa-solid fa-star"></i>
                <span>Red Rocks concerts are legendary experiences! Bring layers - mountain evenings get cool even in summer.</span>
              </div>
              <div class="button-group">
                <a href="https://www.redrocksonline.com/events/big-head-todd-and-the-monsters-817863/" target="_blank" class="link-button mountain-button">
                  <i class="fa-solid fa-ticket"></i> Concert Details
                </a>
                <a href="https://www.redrocksonline.com/" target="_blank" class="link-button">
                  <i class="fa-solid fa-info"></i> Red Rocks Info
                </a>
                <a href="https://www.bigheadtodd.com/" target="_blank" class="link-button">
                  <i class="fa-solid fa-external-link-alt"></i> Band Website
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-bed activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">Late Evening</div>
              <div class="activity-description">Return to La Quinta Littleton after the concert (15-20 minutes from Red Rocks)
                <br><strong>Pro tip:</strong> Traffic exits slowly after concerts - be patient and enjoy the mountain night air!</div>
            </div>
          </li>
        </ul>
      </div>
    </div>

    <!-- Sunday -->
    <div class="day-card" data-day="3">
      <div class="day-header" onclick="toggleDay(this)">
        <div class="day-title">
          <i class="fa-solid fa-plane day-icon"></i>
          <span>Sunday, June 8 – Departure Day: Littleton → Fort Worth</span>
        </div>
        <i class="fa-solid fa-chevron-down expand-icon"></i>
      </div>
      <div class="weather-banner">
        <div class="weather-info">
          <i class="fa-solid fa-cloud-sun" style="font-size: 1.8rem;"></i>
          <span class="weather-location">Travel Day Weather</span>
        </div>
        <div class="weather-details">
          <div class="weather-item">
            <i class="fa-solid fa-thermometer-half"></i>
            <span>High: 79°F</span>
          </div>
          <div class="weather-item">
            <i class="fa-solid fa-moon"></i>
            <span>Low: 54°F</span>
          </div>
          <div class="weather-item">
            <i class="fa-solid fa-cloud-sun"></i>
            <span>Partly cloudy</span>
          </div>
          <div class="weather-item">
            <i class="fa-solid fa-road"></i>
            <span>Good driving</span>
          </div>
        </div>
        <a href="https://weather.com/weather/today/l/76179:4:US" target="_blank" class="link-button weather-button">
          <i class="fa-solid fa-external-link-alt"></i> Full Forecast
        </a>
      </div>
      <div class="day-content">
        <ul class="activity-list">
          <li class="activity-item">
            <i class="fa-solid fa-coffee activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">8:00 AM</div>
              <div class="activity-description">Final hotel breakfast and checkout preparation</div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-camera activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">9:00 AM (Optional)</div>
              <div class="activity-description">Quick morning visit to Chatfield State Park (15 minutes from hotel)
                <br>Beautiful lake views with mountain backdrop - perfect for final Colorado photos</div>
              <div class="button-group">
                <a href="https://www.google.com/maps/dir/5669+S+Alkire+St,+Littleton,+CO+80127/Chatfield+State+Park,+Littleton,+CO" target="_blank" class="link-button">
                  <i class="fa-solid fa-map"></i> Chatfield Park
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-sign-out activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">10:00 AM</div>
              <div class="activity-description">Hotel checkout and departure preparation</div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-route activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">10:30 AM</div>
              <div class="activity-description">Begin drive back to Fort Worth</div>
              <div class="route-info">
                <i class="fa-solid fa-route"></i>
                <span>Return route (~650 miles, 9h 45m): C-470 E → I-25 S → I-35 S → I-35W S to Fort Worth</span>
              </div>
              <div class="button-group">
                <a href="https://www.google.com/maps/dir/5669+S+Alkire+St,+Littleton,+CO+80127/5509+Tuxbury+Pond+Dr,+Fort+Worth,+TX" target="_blank" class="link-button">
                  <i class="fa-solid fa-map"></i> Return Route
                </a>
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-gas-pump activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">Suggested Stops</div>
              <div class="activity-description">
                <strong>Lunch Stop:</strong> Colorado Springs, CO (1 hour south)<br>
                <strong>Afternoon Break:</strong> Amarillo, TX (halfway point)<br>
                <strong>Final Stretch:</strong> Arrive Fort Worth by evening
              </div>
            </div>
          </li>
          <li class="activity-item">
            <i class="fa-solid fa-home activity-icon"></i>
            <div class="activity-content">
              <div class="activity-time">8:00-9:00 PM</div>
              <div class="activity-description">Arrive home at 5509 Tuxbury Pond Dr, Fort Worth, TX</div>
            </div>
          </li>
        </ul>
      </div>
    </div>

    <!-- Tips Section -->
    <div class="tips-section">
      <div class="tips-title">
        <i class="fa-solid fa-mountain"></i>
        <span>Colorado Adventure Tips</span>
      </div>
      <div class="tips-grid">
        <div class="tip-item">
          <i class="fa-solid fa-thermometer-half tip-icon"></i>
          <div class="tip-text">Pack layers! Colorado weather changes quickly. Bring jackets for cool mornings and evenings.</div>
        </div>
        <div class="tip-item">
          <i class="fa-solid fa-droplet tip-icon"></i>
          <div class="tip-text">Stay hydrated at altitude (5,280+ ft). Drink plenty of water and limit alcohol first day.</div>
        </div>
        <div class="tip-item">
          <i class="fa-solid fa-hiking tip-icon"></i>
          <div class="tip-text">Comfortable hiking shoes for Red Rocks trails. Trails can be rocky and steep.</div>
        </div>
        <div class="tip-item">
          <i class="fa-solid fa-sun tip-icon"></i>
          <div class="tip-text">Strong UV rays at altitude - bring sunscreen (SPF 30+), sunglasses, and hat.</div>
        </div>
        <div class="tip-item">
          <i class="fa-solid fa-gas-pump tip-icon"></i>
          <div class="tip-text">Keep gas tank above half full. Mountain driving uses more fuel than Texas plains.</div>
        </div>
        <div class="tip-item">
          <i class="fa-solid fa-music tip-icon"></i>
          <div class="tip-text">For Red Rocks concert: Bring layers (gets cool at night), comfortable shoes for steps, and arrive early for parking!</div>
        </div>
        <div class="tip-item">
          <i class="fa-solid fa-camera tip-icon"></i>
          <div class="tip-text">Bring camera/phone chargers! Colorado's scenery is incredibly photogenic.</div>
        </div>
        <div class="tip-item">
          <i class="fa-solid fa-car tip-icon"></i>
          <div class="tip-text">Check tire pressure before mountain driving. Lower air pressure at altitude affects performance.</div>
        </div>
        <div class="tip-item">
          <i class="fa-solid fa-clock tip-icon"></i>
          <div class="tip-text">Colorado is 1 hour behind Texas (Mountain Time). Adjust plans accordingly.</div>
        </div>
      </div>
    </div>

    <!-- Scroll to top button -->
    <button class="scroll-top" id="scrollTopBtn" onclick="scrollToTop()">
      <i class="fa-solid fa-chevron-up"></i>
    </button>
  </div>

  <script>
    // Mobile-specific interactions
    let isMobile = window.innerWidth <= 768;
    
    window.addEventListener('resize', function() {
      isMobile = window.innerWidth <= 768;
    });

    // Toggle day cards
    function toggleDay(header) {
      const card = header.closest('.day-card');
      card.classList.toggle('expanded');
      
      // On mobile, scroll the expanded card into view
      if (isMobile && card.classList.contains('expanded')) {
        setTimeout(() => {
          card.scrollIntoView({ 
            behavior: 'smooth', 
            block: 'start',
            inline: 'nearest'
          });
        }, 300);
      }
      
      // Update scroll progress when expanding/collapsing
      setTimeout(updateScrollProgress, 300);
    }

    // Scroll progress indicator
    function updateScrollProgress() {
      const winScroll = document.body.scrollTop || document.documentElement.scrollTop;
      const height = document.documentElement.scrollHeight - document.documentElement.clientHeight;
      const scrolled = (winScroll / height) * 100;
      document.getElementById('progressBar').style.width = scrolled + '%';
    }

    // Scroll to top functionality
    function scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
    }

    // Show/hide scroll to top button
    function toggleScrollTopButton() {
      const scrollTopBtn = document.getElementById('scrollTopBtn');
      if (document.body.scrollTop > 300 || document.documentElement.scrollTop > 300) {
        scrollTopBtn.classList.add('visible');
      } else {
        scrollTopBtn.classList.remove('visible');
      }
    }

    // Event listeners
    window.addEventListener('scroll', function() {
      updateScrollProgress();
      toggleScrollTopButton();
    });

    // Initialize on page load
    document.addEventListener('DOMContentLoaded', function() {
      // Open first day by default
      const firstCard = document.querySelector('.day-card[data-day="1"]');
      if (firstCard) {
        firstCard.classList.add('expanded');
      }
      
      updateScrollProgress();
      
      // Add smooth scrolling to all internal links
      document.querySelectorAll('a[href^="#"]').forEach(anchor => {
        anchor.addEventListener('click', function (e) {
          e.preventDefault();
          const target = document.querySelector(this.getAttribute('href'));
          if (target) {
            target.scrollIntoView({
              behavior: 'smooth',
              block: 'start'
            });
          }
        });
      });

      // Add click handlers for activity items to show subtle animation
      document.querySelectorAll('.activity-item').forEach(item => {
        item.addEventListener('click', function() {
          this.style.transform = 'translateX(12px) translateY(-4px)';
          setTimeout(() => {
            this.style.transform = '';
          }, 200);
        });
      });
    });

    // Keyboard navigation
    document.addEventListener('keydown', function(e) {
      // Press 'T' to scroll to top
      if (e.key === 't' || e.key === 'T') {
        if (!e.target.matches('input, textarea')) {
          scrollToTop();
        }
      }
      
      // Press numbers 1-3 to toggle days
      const dayNum = parseInt(e.key);
      if (dayNum >= 1 && dayNum <= 3 && !e.target.matches('input, textarea')) {
        const dayCard = document.querySelector(`.day-card[data-day="${dayNum}"]`);
        if (dayCard) {
          const header = dayCard.querySelector('.day-header');
          toggleDay(header);
          dayCard.scrollIntoView({ behavior: 'smooth', block: 'start' });
        }
      }
    });

    // Add some Easter egg interactions
    let clickCount = 0;
    document.querySelector('header h1').addEventListener('click', function() {
      clickCount++;
      if (clickCount === 5) {
        this.style.animation = 'bounce 1s ease-in-out';
        setTimeout(() => {
          this.style.animation = '';
        }, 1000);
        clickCount = 0;
      }
    });

    // Add bounce animation keyframes
    const style = document.createElement('style');
    style.textContent = `
      @keyframes bounce {
        0%, 20%, 60%, 100% { transform: translateY(0); }
        40% { transform: translateY(-20px); }
        80% { transform: translateY(-10px); }
      }
    `;
    document.head.appendChild(style);
  </script>
</body>
</html>
