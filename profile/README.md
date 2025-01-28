# Fin Ghadi: Your Personalized Activity Guide


## Table of Contents

1. [Fin Ghadi: Your Personalized Activity Guide](#fin-ghadi-your-personalized-activity-guide)
   - [Overview](#overview)
   - [Core Functionalities](#core-functionalities)
     - [1. Geolocation and Weather Data Integration](#1-geolocation-and-weather-data-integration)
     - [2. AI-Driven Activity Suggestions](#2-ai-driven-activity-suggestions)
     - [3. Google Maps Integration](#3-google-maps-integration)
     - [4. Dynamic Suggestions](#4-dynamic-suggestions)
   - [Technology Stack](#technology-stack)
     - [Frontend: Next.js](#frontend-nextjs)
     - [Backend: FastAPI](#backend-fastapi)
     - [APIs and Libraries](#apis-and-libraries)
   - [UI Design (Conception)](#ui-design-conception)
     - [Design Philosophy](#design-philosophy)
     - [Key Features](#key-features)
       - [Swipe-Based Browsing](#swipe-based-browsing)
       - [Visual Appeal](#visual-appeal)
       - [Interactive Elements](#interactive-elements)
       - [Responsive Layout](#responsive-layout)
       - [Weather and Location Display](#weather-and-location-display)
       - [Activity Cards](#activity-cards)
   - [Pipeline Design](#pipeline-design)
     - [Step 1: Collect User Data from UI](#step-1-collect-user-data-from-ui)
     - [Step 2: Fetch Activities Based on User Position](#step-2-fetch-activities-based-on-user-position)
     - [Step 3: Preprocess Data for LLM](#step-3-preprocess-data-for-llm)
     - [Step 4: Generate Suggestions Using LLM](#step-4-generate-suggestions-using-llm)
     - [Step 5: Combine Data for Final Result](#step-5-combine-data-for-final-result)
     - [Step 6: Display Results in UI](#step-6-display-results-in-ui)


## Overview

Imagine an app that instantly knows where you are, understands the weather, and suggests the perfect activity for the moment. Welcome to **Fin Ghadi** ("Where Are You Going?" in Moroccan Darija), a modern, AI-driven web application designed to enrich your experiences. Whether it's a sunny day calling for a park visit or a rainy evening ideal for a cozy café, Fin Ghadi curates activities tailored to your preferences, location, and weather. It's more than just an app—it's your personal concierge for life's adventures.




## Core Functionalities

### 1. Geolocation and Weather Data Integration
- Automatically detects the user's current location using browser-based geolocation.
- Integrates real-time weather data from a trusted weather API to enhance the relevance of activity suggestions.

### 2. AI-Driven Activity Suggestions
- Utilizes Gemini 1.5 Flash to generate unique and contextually relevant activity recommendations based on:
  - Current location
  - Real-time weather conditions
  - Time of day
- Offers varied options including outdoor and indoor activities.

### 3. Google Maps Integration
- Displays the location of suggested activities on Google Maps.
- Takes into account factors such as opening hours to ensure the feasibility of recommendations.

### 4. Dynamic Suggestions
- Ensures that activity suggestions are dynamic and avoid repetition.
- Adapts recommendations based on user feedback and interactions to offer increasingly personalized suggestions.


## Technology Stack

### Frontend: **Next.js**
- Framework for creating a fast, responsive, and SEO-friendly UI.
- Delivers a dynamic user interface with support for real-time updates and smooth animations.

### Backend: **FastAPI**
- Lightweight and efficient backend framework for handling API requests.
- Ensures fast response times and seamless integration with external services (e.g., weather and mapping APIs).

### Frontend mobile: **react nativ **

### APIs and Libraries:
- **OpenWeather API**: For real-time weather data.
- **Google Maps API**: For location visualization and directions.
- **Gemini 1.5 Flash**: To generate AI-powered, personalized activity recommendations.


## UI Design (Conception)

### Design Philosophy
- **Accessible, intuitive, and engaging.**
- Focus on simplicity and ease of use for users of all tech skill levels.

### Key Features
1. **Swipe-Based Browsing**  
   - Users can swipe left or right to browse through activity suggestions.
   - Alternative: Button-based navigation for users who prefer a more traditional interface.

2. **Visual Appeal**  
   - Clean, modern design with smooth transitions and animations.
   - Use of vibrant, weather-inspired color schemes (e.g., sunny yellow, rainy blue).

3. **Interactive Elements**  
   - **Like/Dislike Buttons**: Users can quickly provide feedback on suggestions.
   - **Save Button**: Allows users to save activities for later.
   - **Map Integration**: Displays activity locations directly within the app.

4. **Responsive Layout**  
   - Optimized for both mobile and desktop devices.
   - Adapts to different screen sizes and orientations.

5. **Weather and Location Display**  
   - Real-time weather conditions and user location are prominently displayed at the top of the screen.
   - Icons and brief descriptions make it easy to understand at a glance.

6. **Activity Cards**  
   - Each activity is presented as a card with:
     - A title (e.g., "Visit a Local Park").
     - A brief description.
     - A relevant image or icon.
     - Distance and estimated travel time.

---

## Pipeline Design

### Step 1: Collect User Data from UI
The app collects the following data from the user interface (UI):
- **Timestamp**: Current date and time.
- **Weather Status**: Real-time weather conditions (e.g., sunny, rainy, temperature).
- **User Position**: Latitude and longitude fetched via geolocation.
- **User Demographics**: Sex and age (optional, provided by the user).
- **Location**: User's current location or a specified area of interest.

---

### Step 2: Fetch Activities Based on User Position
- **Zone of Interest**: Define a radius around the user's position to limit the search area.
- **Activity Data**: Fetch activities within the defined radius using the **Google Maps API** or similar services.
  - **Fields Retrieved**:
    - Name of the activity.
    - Type of activity (e.g., park, café, museum).
    - Opening hours.
    - Rating (if available).
    - Distance from the user's location.

---

### Step 3: Preprocess Data for LLM
To reduce the token size sent to the LLM, preprocess the data by:
1. **Filtering Relevant Fields**:
   - Keep only essential information such as:
     - Activity name.
     - Type.
     - Opening hours.
     - Rating.
     - Distance.
2. **Structuring Data**:
   - Format the data into a concise JSON or text format for efficient processing.
3. **Adding Context**:
   - Include user-specific details (e.g., sex, age, weather, timestamp) to provide context for the LLM.

---

### Step 4: Generate Suggestions Using LLM
- **Input to LLM**:
  - Preprocessed activity data.
  - User-specific details (sex, age, weather, timestamp).
- **LLM Task**:
  - Analyze the input and generate the most suitable activity suggestions.
  - Add new fields to the output:
    - **AI Rating**: A score or rating assigned by the LLM based on relevance.
    - **Description**: A brief description of why the activity is recommended.
    - **Construction**: Additional details or tips for the user (e.g., "Great for a sunny afternoon").
- **Output**:
  - A list of recommended activities with the following fields:
    - Name.
    - Type.
    - Opening hours.
    - Rating.
    - Distance.
    - AI Rating.
    - Description.
    - Construction.

---

### Step 5: Combine Data for Final Result
- **Merge Fields**:
  - Combine the original activity data (from Google Maps API) with the AI-generated fields (AI Rating, Description, Construction).
- **Final Output**:
  - A curated list of activities with all relevant details, ready to be displayed in the UI.

---

### Step 6: Display Results in UI
- **Activity Cards**:
  - Each activity is displayed as a card with:
    - Name.
    - Type.
    - Opening hours.
    - Rating (user + AI).
    - Distance.
    - Description and construction (AI-generated).
    - Google Maps integration for location visualization.
- **User Interaction**:
  - Users can:
    - Swipe through activities.
    - Like, dislike, or save suggestions.
    - View detailed information about each activity.

