# DocLink - Digitizing Primary Healthcare in Pakistan

<div align="center">

**Connecting You to Your Own Doctor - 24/7**

[![Next.js](https://img.shields.io/badge/Next.js-12.3.1-black?logo=next.js)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-17-blue?logo=react)](https://reactjs.org/)
[![Material-UI](https://img.shields.io/badge/MUI-5-007FFF?logo=mui)](https://mui.com/)
[![License](https://img.shields.io/badge/license-Private-red)]()

[About](#about) • [Features](#features) • [Getting Started](#getting-started) • [Documentation](#documentation) • [Contributing](#contributing)

</div>

---

## About

DocLink is a comprehensive digital healthcare platform revolutionizing primary healthcare delivery in Pakistan. We connect patients with qualified doctors through a subscription-based model, making healthcare affordable, accessible, and available 24/7.

### Mission

To connect the entire population of Pakistan with their own Doctors, providing seamless healthcare access at minimum cost.

### Vision

To build a subscription-based digital healthcare system in Pakistan, making healthcare affordable and accessible to all.

### Tagline

**"Kabhi Bhi, Kahin Bhi, Rahein Connected 24/7"**  
*Stay Connected Anytime, Anywhere 24/7*

---

## Features

### 🏥 Subscription Plans
- **24/7 Doctor Access**: Stay connected with your own doctor anytime
- **Affordable Pricing**: Starting at PKR 699 with up to 50% off
- **Unlimited Consultations**: Chat, audio, or video consultations
- **Digital Prescriptions**: Instant digital prescriptions

### 🧪 Lab Tests
- **Trusted Labs**: Network of verified laboratory partners
- **Discounted Rates**: Save up to 50% on lab tests
- **Home Collection**: Sample collection at your doorstep
- **Digital Reports**: Instant digital lab reports

### 📋 Medical Records
- **Secure Storage**: Cloud-based secure document storage
- **Easy Access**: Access records anytime, anywhere
- **Share with Doctors**: Instantly share with healthcare providers
- **Complete History**: Organized chronological medical history

### 👨‍⚕️ Doctor Network
- **Verified Doctors**: All doctors are verified professionals
- **Multiple Specialties**: Wide range of medical specialties
- **Patient Reviews**: Read reviews from other patients
- **Easy Booking**: Simple appointment scheduling

### 📱 Mobile Applications
- **Patient App**: Available on Google Play Store
- **Doctor App**: For healthcare providers
- **Video Consultations**: High-quality video calls
- **Chat Support**: Text-based consultations

### 📝 Health Blog
- **Educational Content**: Expert health and wellness articles
- **Regular Updates**: Fresh content added regularly
- **Expert Writers**: Written by healthcare professionals
- **Multiple Categories**: Health tips, nutrition, mental health, and more

---

## Getting Started

### Prerequisites

- **Node.js**: v14.x or higher (recommended: v16.x or v18.x)
- **npm**: v6.x or higher
- **Git**: For version control

### Quick Start

```bash
# Clone the repository
git clone https://github.com/feditech/doclink-web.git
cd doclink-web

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local
# Edit .env.local with your configuration

# Start development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the application.

### Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server on port 3000 |
| `npm run build` | Create optimized production build |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint to check code quality |
| `npm run export` | Export app as static HTML |

---

## Technology Stack

### Core Technologies
- **Framework**: [Next.js 12.3.1](https://nextjs.org/) - React framework with SSR
- **UI Library**: [React 17](https://reactjs.org/) - Component-based UI
- **UI Components**: [Material-UI v5](https://mui.com/) - Comprehensive component library
- **State Management**: [Redux](https://redux.js.org/) with Redux Thunk
- **Styling**: Styled Components + Emotion + Sass

### Key Libraries
- **HTTP Client**: Axios
- **Animations**: Framer Motion
- **Media Player**: React Player
- **Notifications**: React Hot Toast, React Toastify
- **Date Handling**: Moment.js, date-fns
- **Carousel**: React Slick
- **Scrolling**: React Scroll

---

## Documentation

Comprehensive documentation is available in the `docs/` directory:

### 📚 Core Documentation

- **[Project Overview](./docs/PROJECT_OVERVIEW.md)** - Introduction, mission, vision, and technology stack
- **[Getting Started Guide](./docs/GETTING_STARTED.md)** - Installation, setup, and configuration
- **[Architecture Documentation](./docs/ARCHITECTURE.md)** - Technical architecture and design patterns
- **[Features Documentation](./docs/FEATURES.md)** - Detailed feature descriptions
- **[User Guide](./docs/USER_GUIDE.md)** - End-user documentation

### 👩‍💻 Developer Documentation

- **[Development Guide](./docs/DEVELOPMENT.md)** - Development workflow and best practices
- **[API Documentation](./docs/API_DOCUMENTATION.md)** - API endpoints and integration
- **[Contributing Guidelines](./docs/CONTRIBUTING.md)** - How to contribute to the project
- **[Deployment Guide](./docs/DEPLOYMENT.md)** - Deployment instructions and options

### Quick Links

- **Setup**: See [Getting Started Guide](./docs/GETTING_STARTED.md)
- **Architecture**: See [Architecture Documentation](./docs/ARCHITECTURE.md)
- **API Reference**: See [API Documentation](./docs/API_DOCUMENTATION.md)
- **Contributing**: See [Contributing Guidelines](./docs/CONTRIBUTING.md)

---

## Project Structure

```
doclink-web/
├── components/         # React components
│   ├── header/        # Header components
│   ├── footer/        # Footer variations
│   ├── home/          # Home page components
│   ├── aboutus/       # About us components
│   └── ...            # Other feature components
├── pages/             # Next.js pages (routes)
│   ├── index.js       # Home page
│   ├── about-us/      # About us page
│   ├── doctors/       # Doctors listing
│   ├── blogs/         # Health blogs
│   └── ...            # Other pages
├── public/            # Static assets
│   └── assets/        # Images, fonts, icons
├── redux/             # Redux store
├── restApis/          # API configurations
├── styles/            # Global styles
├── utils/             # Utility functions
└── docs/              # Documentation
```

For detailed structure, see [Architecture Documentation](./docs/ARCHITECTURE.md).

---

## Contributing

We welcome contributions from the community! Please read our [Contributing Guidelines](./docs/CONTRIBUTING.md) before submitting pull requests.

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow the [Development Guide](./docs/DEVELOPMENT.md)
- Adhere to coding standards in [Contributing Guidelines](./docs/CONTRIBUTING.md)
- Write clean, documented code
- Test thoroughly before submitting

---

## Deployment

DocLink can be deployed to various platforms:

- **Vercel** (Recommended) - Optimized for Next.js
- **Netlify** - Static site hosting
- **AWS** - Amplify or Elastic Beanstalk
- **Docker** - Container deployment
- **Traditional Node.js** - Any VPS or dedicated server

For detailed deployment instructions, see [Deployment Guide](./docs/DEPLOYMENT.md).

---

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

---

## Security

- End-to-end encryption for sensitive data
- Industry-standard compliant data storage
- Secure authentication and authorization
- Regular security audits

For security concerns, please contact: security@doclink.com

---

## Support

### For Users
- **Email**: support@doclink.com
- **Phone**: +92-XXX-XXXXXXX
- **User Guide**: See [User Guide](./docs/USER_GUIDE.md)
- **FAQs**: Visit the FAQ section on the website

### For Developers
- **Issues**: GitHub Issues for bug reports
- **Discussions**: GitHub Discussions for questions
- **Documentation**: See `docs/` directory
- **Email**: dev@doclink.com

---

## License

This project is private and proprietary. All rights reserved.

---

## Acknowledgments

- Built with [Next.js](https://nextjs.org/)
- UI components from [Material-UI](https://mui.com/)
- Healthcare professionals who guide our mission
- Users who trust DocLink with their healthcare needs

---

## Learn More

### About Next.js

- [Next.js Documentation](https://nextjs.org/docs) - Learn about Next.js features
- [Learn Next.js](https://nextjs.org/learn) - Interactive Next.js tutorial
- [Next.js GitHub](https://github.com/vercel/next.js/) - Next.js repository

### About DocLink

- Visit our website (configured URL)
- Read our [blog posts](./pages/blogs)
- Check out the [About Us](./pages/about-us) page
- Explore [Subscription Plans](./pages/subscription-plans)

---

<div align="center">

**Made with ❤️ for better healthcare in Pakistan**

[Website](#) • [Documentation](./docs/) • [Support](mailto:support@doclink.com)

</div>
