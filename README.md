# Latency Master - GLM Model Performance Tester

A stunning, production-ready single-page application for testing the latency and performance of GLM AI models with real-time visualization, detailed metrics, and user management.

![Latency Master](https://img.shields.io/badge/Version-1.0.0-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)

## 🌟 Features

### Core Functionality
- **🚀 Real-time Latency Testing** - Measure API response times with millisecond precision
- **📊 Live Statistics Dashboard** - View latency, status, response time, tokens, and TPS in real-time
- **⚡ TPS Calculation** - Tokens Per Second calculated using completion tokens for accurate generation speed
- **🎬 Animated Process Timeline** - Visual breakdown of DNS resolution, TLS handshake, request sending, processing, and response receiving
- **👤 User Identity System** - Unique user IDs and random names for multi-user environments
- **🔍 History Filtering** - Filter test results by user ID
- **📝 Test History** - Automatically saves all test results to localStorage (up to 50 tests)
- **🔎 Detailed Views** - Click on any history item to see full details including prompt, response, and timeline breakdown

### User Experience
- **🎨 Beautiful UI** - Modern glassmorphism design with smooth animations
- **🌙 Dark Theme** - Easy on the eyes with gradient backgrounds
- **📱 Responsive Design** - Works perfectly on desktop and mobile devices
- **💾 Persistent Storage** - API key, user identity, and test history saved locally
- **⚡ Instant Feedback** - Real-time updates during test execution

## 📋 Supported GLM Models

| Model | Concurrency | Description |
|-------|-------------|-------------|
| GLM-4.6 | 3 | Standard model |
| GLM-4.6V-FlashX | 3 | Fast variant |
| GLM-4.7 | 5 | Latest version |
| GLM-4.5 | 10 | Balanced model |
| GLM-4.6V | 10 | Vision capable |
| GLM-4-Plus | 20 | High performance |
| GLM-4.5V | 10 | Vision capable |
| GLM-4.6V-Flash | 3 | Fast variant |
| AutoGLM-Phone-Multilingual | 5 | Multilingual |
| GLM-4.5-Air | 5 | Lightweight |
| GLM-4.5-AirX | 5 | Enhanced lightweight |
| GLM-4.5-Flash | 2 | Ultra-fast |
| GLM-4-32B-0414-128K | 15 | Large context |

## 🔬 How It Works

### Architecture Overview

```
User Input → API Request → Process Timeline → Response Analysis → History Storage
     ↓              ↓              ↓                  ↓                  ↓
  Prompt         Fetch API    DNS/TLS/Send/     Extract Data      localStorage
  API Key        Z.AI Endpoint  Process/Receive   TPS Calculation   (50 max)
  Model          Authorization  Animation         Response Text      User ID
  JSON Body      Real-time UI      Token Count       Filter by User
```

### Process Timeline Breakdown

The application visualizes the complete request lifecycle with 5 distinct phases:

1. **DNS Resolution** (~20-70ms)
   - Resolves the API domain to an IP address
   - Simulated with random delay for visualization

2. **TLS Handshake** (~50-150ms)
   - Establishes secure encrypted connection
   - Certificate verification and key exchange
   - Simulated with random delay for visualization

3. **Sending Request** (~10-40ms)
   - Serializes request data to JSON
   - Transmits HTTP POST request
   - Simulated with random delay for visualization

4. **Processing** (Variable)
   - Actual API processing time
   - Model inference and token generation
   - Measured from request send to response receive

5. **Receiving Response** (~Variable)
   - Receives and parses JSON response
   - Extracts content and metadata
   - Measured from response start to completion

### TPS (Tokens Per Second) Calculation

**Formula:**
```
TPS = Completion Tokens / (Latency / 1000)
```

**Why Completion Tokens?**
- `total_tokens` = `prompt_tokens` + `completion_tokens`
- Using total_tokens would inflate TPS because it includes input tokens
- Completion tokens represent actual model generation speed
- Provides accurate measure of model output performance

**Example:**
```
Prompt Tokens: 33
Completion Tokens: 500
Total Tokens: 533
Latency: 2000ms

TPS = 500 / (2000 / 1000) = 500 / 2 = 250 tokens/second
```

### Response Extraction Logic

The application handles multiple response formats from the API:

```javascript
// Priority order for response extraction
1. message.content (standard response)
2. choices[0].text (alternative format)
3. choices[0].delta.content (streaming format)
4. data.content (direct content field)
5. data.output (output field)
6. Raw string response
```

The application automatically detects and extracts the correct field.

### User Identity System

**Generation Process:**
1. Check localStorage for existing user ID
2. If not found, generate unique ID: `user_[timestamp][random]`
3. Generate random name from adjective + noun combinations
4. Store in localStorage for persistence

**User ID Format:**
```
user_1a2b3c4d5e6f7g8h9i0j1k
```

**Random Names Examples:**
- SwiftRunner
- BrightCoder
- QuickNinja
- SmartWizard
- FrostMaster

**Avatar Display:**
- Gradient circle with user's first initial
- User name displayed
- Last 8 characters of user ID shown

### History Management

**Storage Structure:**
```javascript
{
  id: 1234567890,
  timestamp: "2026-01-05T08:00:00.000Z",
  model: "GLM-4.7",
  prompt: "Explain machine learning...",
  response: "Machine learning is...",
  latency: 2000,
  tokens: 533,
  tps: "250.00",
  status: "success",
  timeline: {
    dns: 45,
    tls: 150,
    send: 180,
    process: 1800,
    receive: 2000
  },
  userId: "user_1a2b3c4d",
  userName: "SwiftRunner"
}
```

**Filtering:**
- Filter by specific user ID
- View all users' tests
- Dropdown auto-updates when new users appear

**Retention:**
- Maximum 50 tests stored
- Oldest tests removed when limit exceeded
- Persistent across sessions

## 🚀 Getting Started

### Prerequisites

- Modern web browser (Chrome, Firefox, Safari, Edge)
- Valid Z.AI API key from [z.ai](https://z.ai)

### Installation

1. **Clone or Download**
   ```bash
   git clone https://github.com/yourusername/latency-master.git
   cd latency-master
   ```

2. **Open in Browser**
   - Simply open `index.html` in your web browser
   - No build process or dependencies required

3. **Or Use a Local Server** (Optional)
   ```bash
   # Using Python 3
   python -m http.server 8000
   
   # Using Node.js
   npx serve
   
   # Using PHP
   php -S localhost:8000
   ```
   Then visit `http://localhost:8000`

### Usage

1. **Enter API Key**
   - Get your API key from [Z.AI](https://z.ai)
   - Paste it in the "API Key" field
   - Key is automatically saved for future visits

2. **Select Model**
   - Choose from the dropdown list
   - See concurrency limits for each model

3. **Enter Prompt**
   - Type your test prompt
   - Or click "Use Sample Prompt" for a quick test
   - Character counter shows prompt length

4. **Run Test**
   - Click "Run Latency Test"
   - Watch the animated process timeline
   - View real-time statistics

5. **View Results**
   - See live stats update in real-time
   - Model response appears automatically
   - Check history for past tests
   - Click any history item for detailed view

6. **Filter History**
   - Use dropdown to filter by user
   - View all users or specific user
   - See test count for current filter

## 🏗️ Technical Details

### Technology Stack

- **HTML5** - Structure and semantics
- **CSS3** - Styling with Tailwind CSS (via CDN)
- **Vanilla JavaScript** - No frameworks or dependencies
- **localStorage API** - Persistent storage
- **Fetch API** - HTTP requests
- **Performance API** - Precise timing measurements

### Performance Optimizations

- **Debounced Input** - Prevents excessive re-renders
- **Efficient DOM Updates** - Minimal reflows
- **CSS Animations** - Hardware-accelerated
- **Lazy Loading** - History rendered on demand
- **LocalStorage Caching** - Reduces API calls

### Browser Compatibility

- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Mobile browsers (iOS Safari, Chrome Mobile)

### Storage Limits

- **localStorage**: ~5-10MB (varies by browser)
- **Test History**: 50 tests max
- **API Key**: Persistent
- **User Identity**: Persistent

## 📊 Metrics Explained

### Latency
- **Definition**: Total time from request start to response completion
- **Measurement**: `performance.now()` in milliseconds
- **Good**: <1000ms | **Warning**: 1000-3000ms | **Poor**: >3000ms

### TPS (Tokens Per Second)
- **Definition**: How many tokens the model generates per second
- **Formula**: `completion_tokens / (latency / 1000)`
- **Higher is better**: Indicates faster generation speed

### Tokens
- **Total Tokens**: Input + output tokens
- **Completion Tokens**: Only output tokens
- **Affects**: TPS calculation and API cost

### Timeline Breakdown
- **DNS**: Domain resolution time
- **TLS**: Secure connection establishment
- **Send**: Request transmission time
- **Process**: Actual model processing time
- **Receive**: Response download time

## 🔐 Security Considerations

- **API Key Storage**: Stored in localStorage (client-side only)
- **No Server**: No backend, data never leaves your browser
- **HTTPS Recommended**: Use HTTPS in production
- **Local Testing**: Safe for local development
- **API Key Protection**: Never logged or transmitted to third parties

## 🌐 Deployment

### GitHub Pages

1. Push to GitHub repository
2. Enable GitHub Pages in repository settings
3. Select `main` branch as source
4. Access at `https://username.github.io/latency-master`

### Netlify

1. Drag and drop the folder to Netlify
2. Or connect to GitHub repository
3. Automatic deployment on push

### Vercel

1. Import project from GitHub
2. Automatic deployment
3. Custom domain support

### Static Hosting

Works on any static hosting service:
- AWS S3 + CloudFront
- Firebase Hosting
- Cloudflare Pages
- Any web server

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

### Development Setup

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- [Z.AI](https://z.ai) for the GLM API
- [Tailwind CSS](https://tailwindcss.com) for the utility-first CSS framework
- The open-source community

## 📧 Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Check existing issues for solutions
- Read the documentation thoroughly

## 🗺️ Roadmap

- [ ] Export test results to CSV/JSON
- [ ] Compare multiple test runs
- [ ] Custom model endpoints
- [ ] Batch testing mode
- [ ] Graphical performance trends
- [ ] Dark/Light theme toggle
- [ ] More detailed error handling
- [ ] WebSocket support for real-time streaming

---

**Made with ❤️ for the AI community**

*Test your GLM models with precision and style!*
