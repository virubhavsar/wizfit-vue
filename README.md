# WizFit

This is a Vue.js-based application for the WizFit Challenge.

### Note: The font style will change as per the client's requirements.

## Project Setup

### 1. Clone the Repository

Clone the repository to your local machine using the following command:

```bash
git clone https://github.com/virubhavsar/wizfit-vue.git
cd wizfit-vue
```

### 2. Install Dependencies

Install the required dependencies with npm:

```bash
npm install
```

### 3. Compile and Hot-Reload for Development

Start the development server with hot-reload enabled by running:

```bash
npm run dev
```

### Folder Structure

```bash

wizfit-vue/
├── public/                # Static files and assets
│   └── index.html         # Main HTML file
├── src/                   # Source code for the Vue.js application
│   ├── assets/            # Application-specific assets
│   │   ├── css/           # CSS files
│   │   │   └── WizFitChallenge.css  # Main CSS file for styling
│   │   └── img/           # Images used in the application
│   │       └── apple-store.png
            └── banner.png
            └── google-store.png
            └── no_img.png
            └── player.png
│   ├── components/        # Vue components for the UI
│   │   └── SchoolList.vue # Component for displaying the list of schools
│   ├── config/            # Configuration files
│   │   └── config.js      # Configuration file for API endpoints
│   ├── views/             # View components for different pages
│   │   └── Home.vue       # Home view component
│   ├── App.vue            # Root component
│   └── main.js            # Entry point for the application
├── .env                   # Environment variables configuration
├── .gitignore             # Ignored files in version control
├── package.json           # Project metadata and dependencies
└── README.md              # Project documentation (this file)

```
