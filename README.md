# GeoGuesser

A geography guessing game where you're given clues about a mystery country — its capital, languages, population, and name length — and have to click the right spot on the world map. Built with Next.js, TypeScript, and Firebase. (Turns out guessing where Kyrgyzstan is harder than it sounds.)

## How It Works

1. You're shown a description of a mystery country (capital, spoken languages, population, name hints)
2. Click on the world map where you think it is
3. Submit your guess (you win if you're within range of the country's actual borders)
4. Score tracked across rounds; reset anytime

Scoring uses the Haversine formula to calculate real-world distance between your click and the country's geographic center, with hit tolerance scaled to country size (so yes, Russia is easier to hit than Luxembourg).

## Built With

- **Next.js** (App Router) + **TypeScript**
- **Firebase Auth** — user authentication and session management
- **REST Countries API** — live country data (capitals, languages, population, coordinates)
- **Natural Earth GeoJSON** — geographic boundary data for accurate centroids and hit radii
- Custom **Mercator projection** math to map lat/lng to pixel coordinates

## Features

- 195+ countries pulled live from a public API
- Geographic centroids computed from real boundary polygons — not just a single coordinate
- Hit tolerance dynamically scales with country area (Vatican ≠ Canada)
- Click-to-guess interface with visual pin drop on the map
- Distance feedback on incorrect guesses ("You were ~3,400 km away.")
- Firebase-authenticated sessions

##  Running Locally

```bash
git clone https://github.com/mboult1/geoguesser
cd geoguesser
npm install
```

Add a `.env.local` file with your Firebase config:

```
NEXT_PUBLIC_FIREBASE_API_KEY=...
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=...
NEXT_PUBLIC_FIREBASE_PROJECT_ID=...
```

Then:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) and start guessing.

---

## The Math

Country hit detection uses a two-step approach:
1. **Haversine formula** calculates great-circle distance (km) between the clicked point and the country's centroid
2. **Hit radius** is derived from the country's actual GeoJSON boundary polygon — not estimated from area — with a minimum floor of 1,000 km so small countries are still playable

---

*Built as a personal project. Geography knowledge not included.*
