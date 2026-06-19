# 💧 AquaTrack

AquaTrack is a cross-platform hydration-tracking mobile app built with **React Native** and **Expo**. It lets users log their daily water intake and dynamically adjusts their hydration goal using **real-time weather data** from the **Open-Meteo API** — so on hot days, the app recommends drinking more.

Built as a rapid hackathon-style prototype focused on a clean core experience: log water, see live weather, get a smarter daily target.

## ✨ Features

- **Quick water logging** — one-tap buttons to add 250ml / 500ml / 750ml to your daily total
- **Live weather integration** — pulls current temperature and conditions from [Open-Meteo](https://open-meteo.com/) based on device location
- **Dynamic hydration goal** — baseline goal calculated from body weight (~35ml/kg), automatically increased on hot or humid days
- **Persistent daily tracking** — intake is saved locally with `AsyncStorage` and resets automatically each new day
- **Graceful fallback** — if location permission is denied or the weather API is unreachable, the app still works using a weight-based baseline goal

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Framework | React Native (Expo) |
| Location | `expo-location` |
| Weather API | [Open-Meteo](https://open-meteo.com/) (no API key required) |
| Persistence | `@react-native-async-storage/async-storage` |
| Language | JavaScript (ES6+) |

## 📂 Project Structure

```
AquaTrack_App/
├── App.js                          # App entry point
├── app.json                        # Expo configuration
├── babel.config.js                 # Babel/Expo preset config
├── package.json                    # Dependencies & scripts
└── src/
    ├── screens/
    │   └── HomeScreen.js           # Main screen: weather, progress, logging
    ├── components/
    │   ├── ProgressBar.js          # Visual intake-vs-goal progress bar
    │   └── IntakeButton.js         # Quick-add water buttons
    ├── services/
    │   ├── weatherService.js       # Open-Meteo API calls
    │   └── storageService.js       # AsyncStorage read/write helpers
    └── utils/
        └── hydrationCalculator.js  # Weight + weather → daily goal logic
```

## 🚀 Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v18+ recommended)
- [Expo Go](https://expo.dev/go) app on your phone, **or** an Android/iOS simulator
- VS Code (or any editor)

### Setup

```bash
# Clone the repo
git clone https://github.com/aakashsapatnekar/AquaTrack_App.git
cd AquaTrack_App

# Install dependencies
npm install

# Start the Expo development server
npm start
```

Then scan the QR code with the **Expo Go** app on your phone, or press `a` / `i` in the terminal to launch an Android/iOS simulator.

> 📍 On first launch, allow location access so AquaTrack can fetch local weather. If denied, the app still works using a weight-based goal only.

## 🧠 How the Goal Is Calculated

1. **Baseline**: `weight (kg) × 35ml`
2. **Heat adjustment**: if current temperature > 25°C, add `60ml` per degree over the threshold
3. **Humidity bonus**: on hot days with a high chance of precipitation, add a flat `150ml`

This logic lives in `src/utils/hydrationCalculator.js` and is fully unit-testable in isolation from the UI.

## 🔮 Possible Future Enhancements

- Hydration history & streak tracking
- Local push notifications for reminders (with quiet hours)
- Multi-day charts and trends
- Custom intake amounts and container presets

## 👤 Author

**Aakash Sapatnekar**
GitHub: [@aakashsapatnekar](https://github.com/aakashsapatnekar)

## 📄 License

This project is open source and available for personal/educational use.
