# Movie App

A modern, responsive movie application built with Vue.js 3 and Vite. This application provides an elegant interface for browsing movies, viewing schedules, and exploring cinema information.

## Features

- **Responsive Design**: Optimized for desktop, tablet, and mobile devices
- **Modern UI**: Clean, cinema-themed interface with smooth animations
- **Navigation**: Sticky header with responsive hamburger menu
- **Multiple Sections**: Home, Screens, Schedule, Movie Library, Location & Contact, Gallery
- **Touch-Friendly**: Optimized for touch devices with proper hover states

## Tech Stack

- **Frontend Framework**: Vue.js 3 (Composition API)
- **Build Tool**: Vite
- **Styling**: CSS3 with custom responsive design
- **Icons & Assets**: SVG icons and custom logos

## Project Structure

```
my-movie-app/
├── public/
├── src/
│   ├── assets/
│   │   ├── css/
│   │   │   └── global.css
│   │   ├── Icons/
│   │   │   ├── ...│   
│   │   ├── Images/
│   │   │   ├── ...
│   │   └── Logos/
│   │   │    └── ...
│   │   ├── Videos/
│   │   │   ├── ...
│   ├── components/
│   │   └── ...
│   ├── App.vue
│   ├── main.js
│   └── style.css
├── index.html
├── package.json
├── vite.config.js
└── README.md
```

## Getting Started

### Prerequisites

- Node.js (version 16 or higher)
- npm or yarn package manager

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd my-movie-app
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:5173`

### Build for Production

```bash
npm run build
```

The built files will be in the `dist` directory.

### Preview Production Build

```bash
npm run preview
```

## Components

### Header Component
- Responsive navigation with hamburger menu
- Sticky positioning
- Adaptive menu items based on screen size
- Smooth animations and transitions
- Touch-friendly interactions

## Responsive Breakpoints

- **Large Desktop**: ≥1200px - Full navigation with gallery in hamburger menu
- **Tablet Landscape**: 992px-1199px - Condensed nav with location/contact in hamburger
- **Tablet Portrait**: 769px-991px - Main nav items with additional items in hamburger
- **Mobile Landscape**: 481px-768px - Hamburger-only navigation
- **Mobile Portrait**: ≤480px - Compact hamburger navigation
- **Extra Small**: ≤360px - Optimized for small screens

## Styling Guidelines

- **Color Scheme**: Black background (#000) with white text (#fff)
- **Borders**: Subtle gray borders (#252424)
- **Typography**: Clean, readable fonts with proper sizing hierarchy
- **Spacing**: Consistent padding and margins across breakpoints
- **Animations**: Smooth 0.3s transitions for interactive elements

## Browser Support

- Modern browsers (Chrome, Firefox, Safari, Edge)
- Mobile browsers (iOS Safari, Chrome Mobile)
- Responsive design tested across various screen sizes

## Development

### Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run linter (if configured)

### Code Style

- Vue 3 Composition API
- Scoped CSS styling
- Semantic HTML structure
- Mobile-first responsive design
- Accessible markup and interactions
