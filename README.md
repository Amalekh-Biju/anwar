# Anwar Sports Arena - Event Venue Website

A modern, responsive website for **Anwar Sports Arena**, a versatile event venue perfect for weddings, parties, corporate events, and celebrations. Built with Astro, Vue.js, and TailwindCSS for optimal performance and user experience.

## About

Anwar Sports Arena is a stunning event venue featuring professional lighting, sound systems, and spacious layout perfect for memorable occasions. This website showcases the venue's capabilities, services, amenities, and provides booking functionality for events.

### Key Features

- **Responsive Design**: Mobile-first approach with seamless desktop experience
- **Interactive Gallery**: Fullscreen image viewer with navigation
- **Room Booking System**: Detailed room information with direct booking links
- **Activity Showcase**: Local experiences like kayaking, backwater tours, and spa services
- **Social Integration**: Connected with Instagram and Facebook
- **SEO Optimized**: Comprehensive meta tags and structured data
- **Performance Focused**: Built with Astro for lightning-fast loading

## �️ Tech Stack

- **Framework**: [Astro](https://astro.build/) - Static site generator with partial hydration
- **Frontend**: [Vue.js 3](https://vuejs.org/) - Interactive components and dynamic functionality
- **Styling**: [TailwindCSS 4](https://tailwindcss.com/) - Utility-first CSS framework
- **Fonts**: Custom Google Fonts (Raleway, Poppins, Prata)
- **Deployment**: Cloudflare Pages with Cloudflare adapter
- **Development**: TypeScript support with strict configuration

## 📁 Project Structure

```text
anwar-sports-arena/
├── public/                     # Static assets
│   ├── bg.jpg                 # Background image
│   ├── favicon.svg            # Site favicon
│   ├── activites/             # Activity images
│   ├── amenites/              # Amenity icons
│   ├── anwar/                 # Anwar Arena property images
│   ├── celebrate/             # Celebration event images
│   ├── nirmala/               # Nirmala Mansion property images
│   └── thejus/                # Thejus Homes property images & video
├── src/
│   ├── components/            # Vue and Astro components
│   │   ├── Activites/         # Activity showcase components
│   │   ├── Amenites/          # Amenity grid components
│   │   ├── Celebrate/         # Event celebration components
│   │   ├── Gallery/           # Image gallery components
│   │   ├── Reviews/           # Customer review components
│   │   ├── Stays/             # Room booking components
│   │   ├── Contact.astro      # Contact form component
│   │   ├── Footer.astro       # Site footer
│   │   ├── Navbar.vue         # Navigation component
│   │   ├── Photoshoot.astro   # Photoshoot services
│   │   ├── Rudra.astro        # Rudra Properties showcase
│   │   ├── Socials.astro      # Social media links
│   │   ├── AnwarGallery.vue   # Hero image carousel
│   │   └── ThejusContent.astro # About us section
│   ├── data/                  # JSON data files
│   │   ├── activitesdata.json # Activities information
│   │   ├── propertydata.json  # Main property & room data
│   │   ├── propertyies.json   # All Rudra properties
│   │   └── reviewdata.json    # Customer reviews
│   ├── layouts/
│   │   └── Layout.astro       # Base HTML layout
│   ├── pages/
│   │   └── index.astro        # Homepage
│   └── styles/
│       └── global.css         # Global styles and TailwindCSS
├── astro.config.mjs           # Astro configuration
├── package.json               # Dependencies and scripts
├── tsconfig.json              # TypeScript configuration
└── README.md                  # Project documentation
```

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed:

- **Node.js** (version 18 or higher)
- **npm** or **yarn** package manager

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/Glitchyi/anwar-sports-arena.git
   cd anwar-sports-arena
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Start the development server**

   ```bash
   npm run dev
   ```

4. **Open your browser**

   Navigate to `http://localhost:4321` to view the website

### Available Scripts

All commands are run from the root of the project:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Install project dependencies                     |
| `npm run dev`             | Start local development server at `localhost:4321` |
| `npm run build`           | Build production site to `./dist/`              |
| `npm run preview`         | Preview build locally before deploying          |
| `npm run astro ...`       | Run Astro CLI commands like `astro add`, `astro check` |

## 🎨 Key Components

### Layout & Navigation

- **Layout.astro**: Base HTML layout with SEO meta tags and background styling
- **Navbar.vue**: Responsive navigation with mobile hamburger menu and scroll-to-top functionality

### Content Sections

- **AnwarGallery.vue**: Hero image carousel with automatic slideshow and navigation controls
- **ThejusContent.astro**: About us section describing the homestay's location and charm
- **StaysContent.astro**: Room showcase with detailed information and booking functionality
- **Amenites.astro**: Grid display of all available amenities with icons
- **Activites.astro**: Horizontal scrolling gallery of available activities
- **Celebrate.astro**: Event hosting capabilities showcase
- **Gallery.astro**: Comprehensive image gallery with fullscreen viewer
- **Reviews.astro**: Customer testimonials with star ratings
- **Contact.astro**: Contact information and direct communication links

### Interactive Features

- **StayCard.vue**: Individual room cards with expandable detailed views
- **KeyCard.vue**: Detailed room information modal with booking functionality
- **GalleryGallery.vue**: Desktop staggered gallery with fullscreen navigation
- **MobileGallery.vue**: Mobile-optimized horizontal scrolling gallery
- **ReviewCard.vue**: Individual review components with star ratings

## 📊 Data Structure

The website uses JSON files for content management:

- **propertydata.json**: Main property information, room details, and images
- **reviewdata.json**: Customer reviews and ratings
- **activitesdata.json**: Available activities and their images
- **propertyies.json**: All Rudra Group properties for cross-promotion

## 🎯 Features Breakdown

### Room Booking System

- Three luxury rooms: Chennellu, Chembavu, and Njavara Royal Suite
- Detailed room descriptions, amenities, and pricing
- Direct booking links integrated with external booking system
- Capacity indicators and premium room highlighting

### Activity & Experience Showcase

- Kayaking and backwater tours
- Nature trail walks and cycling
- Ayurvedic spa services
- Bike rentals and local experiences

### Responsive Design

- Mobile-first approach with progressive enhancement
- Touch-friendly interfaces for mobile devices
- Desktop-optimized layouts for larger screens
- Smooth animations and transitions throughout

### SEO & Performance

- Comprehensive meta tags for social media sharing
- Structured data for search engines
- Optimized images and lazy loading
- Fast loading times with Astro's static generation

## 🌐 Deployment

The project is configured for deployment on **Cloudflare Pages** using the Cloudflare adapter.

### Build for Production

```bash
npm run build
```

### Preview Production Build

```bash
npm run preview
```

The built files will be in the `./dist/` directory, ready for deployment.

## 🔧 Development Notes

### Styling Approach

- **TailwindCSS 4**: Utility-first CSS framework for rapid development
- **Custom CSS**: Global styles in `src/styles/global.css` for brand colors and fonts
- **Typography**: Custom font stack with Raleway (primary), Poppins, and Prata
- **Responsive**: Mobile-first design with `lg:` prefixes for desktop layouts

### Component Architecture

- **Astro Components** (`.astro`): Server-side rendered static content
- **Vue Components** (`.vue`): Interactive client-side functionality
- **Hydration**: Selective hydration with `client:load` directive for performance

### Data Management

- **Static JSON**: All content stored in JSON files for easy maintenance
- **No CMS**: Simple file-based content management for small-scale project
- **Images**: Organized in `/public/` directory by category

## 📱 Browser Support

- **Modern Browsers**: Chrome, Firefox, Safari, Edge (latest versions)
- **Mobile**: iOS Safari, Android Chrome
- **Features**: ES6+, CSS Grid, Flexbox, CSS Custom Properties

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## 📞 Contact & Support

- **Website**: [anwarsportsarena.com](https://anwarsportsarena.com/)
- **Email**: [contact@anwarsportsarena.com](mailto:contact@anwarsportsarena.com)
- **Phone**: [+91 97782 38199](tel:+919778238199)
- **Instagram**: [@anwarsportsarena](https://www.instagram.com/anwarsportsarena/)
- **Facebook**: [Anwar Sports Arena](https://www.facebook.com/anwarsportsarena)

## 📄 License

This project is developed for **Anwar Sports Arena**. All rights reserved.

---

**Powered by [AC Inc.](https://ac-inc.in)** - Professional web development services

Made with ❤️ in Kerala, India
