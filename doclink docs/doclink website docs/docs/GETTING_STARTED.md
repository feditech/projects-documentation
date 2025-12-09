# Getting Started with DocLink

This guide will help you set up the DocLink web application on your local development environment.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Node.js**: Version 14.x or higher (recommended: 16.x or 18.x)
- **npm**: Version 6.x or higher (comes with Node.js)
- **Git**: For cloning the repository

### Verifying Prerequisites

```bash
node --version  # Should output v14.x.x or higher
npm --version   # Should output 6.x.x or higher
git --version   # Should output git version 2.x.x or higher
```

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/feditech/doclink-web.git
cd doclink-web
```

### 2. Install Dependencies

```bash
npm install
```

This will install all required dependencies including:
- Next.js and React
- Material-UI components
- Redux for state management
- Axios for API calls
- And all other dependencies listed in `package.json`

**Note**: You may see some peer dependency warnings. These are generally safe to ignore for development purposes.

### 3. Environment Configuration

Create a `.env.local` file in the root directory for environment-specific variables:

```bash
# API Configuration
NEXT_PUBLIC_API_BASE_URL=your_api_base_url

# Other environment variables as needed
```

**Important**: Never commit `.env.local` or any file containing sensitive information to version control.

## Running the Development Server

Start the development server:

```bash
npm run dev
```

The application will start on [http://localhost:3000](http://localhost:3000).

### What Happens During Development

- **Hot Reload**: Changes to files will automatically reload in the browser
- **Fast Refresh**: React components update without losing state
- **Error Overlay**: Compilation and runtime errors are displayed in the browser

## Building for Production

To create an optimized production build:

```bash
npm run build
```

This command:
1. Compiles and optimizes all pages
2. Generates static HTML for pages where possible
3. Creates optimized JavaScript bundles
4. Processes and optimizes images

### Running Production Build Locally

After building, you can test the production build locally:

```bash
npm run start
```

## Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Starts the development server on port 3000 |
| `npm run build` | Creates an optimized production build |
| `npm run start` | Starts the production server |
| `npm run lint` | Runs ESLint to check code quality |
| `npm run export` | Exports the app as static HTML |

## Project Structure Overview

```
doclink-web/
├── components/        # React components
│   ├── header/       # Header components
│   ├── footer/       # Footer components
│   ├── home/         # Home page components
│   ├── aboutus/      # About us components
│   └── ...           # Other feature components
├── pages/            # Next.js pages (routes)
│   ├── index.js      # Home page
│   ├── about-us/     # About us page
│   ├── subscription-plans/  # Subscription plans
│   └── ...           # Other pages
├── public/           # Static assets
│   └── assets/       # Images, fonts, etc.
├── redux/            # Redux store configuration
├── restApis/         # API endpoint definitions
├── styles/           # Global styles
├── utils/            # Utility functions
└── docs/             # Documentation
```

## First Steps After Setup

1. **Explore the Home Page**: Visit `http://localhost:3000` to see the main landing page
2. **Check Available Routes**: Navigate through different pages:
   - `/about-us` - Learn about DocLink
   - `/subscription-plans` - View subscription options
   - `/doctors` - Browse doctors
   - `/blogs` - Read health blogs
   - `/contact-us` - Contact form

3. **Review Documentation**: Check out the other documentation files:
   - [Architecture](./ARCHITECTURE.md) - Understand the technical structure
   - [Features](./FEATURES.md) - Learn about all features
   - [Development](./DEVELOPMENT.md) - Development workflow and best practices

## Troubleshooting

### Port 3000 Already in Use

If port 3000 is already in use:

```bash
# Kill the process using port 3000 (Linux/Mac)
lsof -ti:3000 | xargs kill

# Or specify a different port
PORT=3001 npm run dev
```

### Module Not Found Errors

If you encounter module not found errors:

```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

### Build Errors

If you encounter build errors:

1. Check that all dependencies are correctly installed
2. Ensure your Node.js version is compatible
3. Clear the Next.js cache: `rm -rf .next`
4. Try rebuilding: `npm run build`

## Getting Help

- Review the [Development Guide](./DEVELOPMENT.md) for detailed development workflows
- Check the [Architecture Documentation](./ARCHITECTURE.md) for technical details
- Consult the [API Documentation](./API_DOCUMENTATION.md) for API integration
- Read the [Contributing Guidelines](./CONTRIBUTING.md) if you plan to contribute

## Next Steps

Once you have the application running:

1. Read the [Features Documentation](./FEATURES.md) to understand what the platform offers
2. Review the [Architecture Guide](./ARCHITECTURE.md) to understand the codebase structure
3. Check the [Development Guide](./DEVELOPMENT.md) for development best practices
4. Explore the [User Guide](./USER_GUIDE.md) to understand the user experience
