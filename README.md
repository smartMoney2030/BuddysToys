# **🧸 Buddy's Consignment Desk (Toybox Valuator)**

An intelligent, AI-powered toy appraisal and consignment calculator built exclusively for **Buddy's Toys and Collectibles**. This responsive application enables boutique toy retailers to photograph toys using their device camera, instantly look up MSRP vs. used market resale benchmarks (powered by Gemini 2.5 Flash), split profits dynamically with consignors, and maintain an exportable session inventory ledger.

## **🚀 Key Features**

* **Scalable Brand Identity**: Includes a highly precise, infinite-resolution vector (SVG) recreation of the iconic yellow, orange, and blue **Buddy's Toys and Collectibles** sticker logo.  
* **Dual-Appraisal Workflow**:  
  * **Camera Scan**: Take a direct photograph using front/back facing mobile cameras or drag-and-drop a high-res JPG.  
  * **Manual Lookup**: Search by keyword or model number when reference photographs aren't readily available.  
* **Market-Matched Analytics**: Leverages advanced computer vision to identify item model structures, release years, current brand MSRPs, and secondary resale average indices (matching active platforms like eBay & Mercari).  
* **Dynamic Split Calculator**:  
  * Interactive range sliders to configure custom split percentages (standard 40% store split vs. 60% consignor split).  
  * Add-on fields to deduct preparation or cleaning fees and processing costs directly from payout channels.  
* **Intake Ledger & Management**: Batch multiple items together under single consignor metadata sheets. Review approved contracts, print summaries, or export session receipts as standardized .csv spreadsheets.

## **💻 Running the Project Locally**

Follow these quick commands to spin up the local development desktop server using React and Vite.

### **Prerequisites**

Make sure you have [Node.js](https://nodejs.org/) (v16+) installed.

### **1\. Clone the Repository**

git clone https://github.com/YOUR\_USERNAME/YOUR\_REPOSITORY.git  
cd YOUR\_REPOSITORY

### **2\. Scaffold Vite Template**

If you only saved the App.jsx file, you can initialize React and Tailwind globally in your folder:

\# Set up React inside the current directory  
npm create vite@latest . \-- \--template react

\# Install base dependencies  
npm install

### **3\. Install App Dependencies**

Install the styling and icons required by the interface:

npm install lucide-react

### **4\. Install & Configure Tailwind CSS**

npm install \-D tailwindcss postcss autoprefixer  
npx tailwindcss init \-p

Update your tailwind.config.js to target your files:

/\*\* @type {import('tailwindcss').Config} \*/  
export default {  
  content: \[  
    "./index.html",  
    "./src/\*\*/\*.{js,ts,jsx,tsx}",  
  \],  
  theme: {  
    extend: {},  
  },  
  plugins: \[\],  
}

Add these Tailwind directives into your ./src/index.css file:

@tailwind base;  
@tailwind components;  
@tailwind utilities;

### **5\. Start App**

Copy the code inside App.jsx from this directory over to your local ./src/App.jsx file, then boot up the dev compiler:

npm run dev

Open **http://localhost:5173** inside your favorite browser\!

## **📱 Packaging as a Native Mobile App (iOS & Android)**

You can convert this project into a mobile application using **Capacitor**—letting you run the application directly on your phone and use the built-in native device cameras.

### **1\. Add Capacitor Core**

Initialize the mobile configuration layers inside your local project:

npm install @capacitor/core @capacitor/cli  
npx cap init

* **App Name**: Buddy's Consignment Desk  
* **Web Asset Directory**: dist (Ensure this points directly to Vite's output compilation directory)

### **2\. Install Platforms**

Install the required platform binaries:

npm install @capacitor/android @capacitor/ios  
npx cap add android  
npx cap add ios

### **3\. Add App Permissions**

Because the application needs to interact directly with hardware cameras, add device usage safety keys:

* **For Android** (./android/app/src/main/AndroidManifest.xml):  
  Add the camera hardware use permission within the root \<manifest\> tag:  
  \<uses-permission android:name="android.permission.CAMERA" /\>

* **For iOS** (Info.plist inside Xcode):  
  Create a key named **Privacy \- Camera Usage Description** and include a short client description:*"Buddy's requires camera access to scan toy packages for secondary market evaluations."*

### **4\. Sync & Open**

Build the compilation assets and copy them straight into your respective native simulators:

\# Compile React static outputs  
npm run build

\# Synchronize static assets into Android & iOS directories  
npx cap sync

\# Open developers workbench  
npx cap open android  
npx cap open ios

Hit the **Play** button in Android Studio or Xcode to compile your installable application package (.apk/.ipa) and test on physical devices\!

## **🔑 Setting up Your Gemini API Key**

The tool runs in "Sandbox Mode" by default. To unlock customized performance, higher analysis boundaries, and bypass limits:

1. Head over to [Google AI Studio](https://aistudio.google.com/) and grab a free or pay-as-you-go developer API Key.  
2. Click **Custom Key Setup** (gear icon) in the top-right corner of the application screen.  
3. Paste your key. It's stored securely in your local browser storage and used solely for direct outbound connections to Google's endpoints.

## **🎨 Design Theme Specs**

* **Primary Accent Color**: \#FC4C02 (Buddy's Vibrant Brand Orange)  
* **Secondary Accent Color**: \#F6E71D (Buddy's Yellow Highlight)  
* **Neutral Charcoal Shield**: \#1A1A1D  
* **Dark Contrast Blue**: \#2B59C3

## **📄 License**

This project is proprietary and custom-tailored for **Buddy's Toys and Collectibles**. Redistribution, reselling, or public deployment of the app files requires explicit authorization.