# 📚 BookSwap - College Android Application

**BookSwap** is an Android application developed as a **university project**.  
It serves as a **mobile marketplace** for students to buy and sell used textbooks — fostering a community of exchange and making educational resources more affordable.

The platform includes features such as user authentication (including Google Sign-In), book listings, profile management, a shopping cart, wishlist functionality, push notifications, multi-language support, and a secure transaction system.  
This project is built using **modern Android development practices** with **Kotlin**, **Firebase**, **Google Books API**, and the **MVVM (Model-View-ViewModel)** architecture.

---
## 🎬 Video Demonstration

A video presentation showcasing the app's features is available at the link below:

[**Click here to watch the BookSwap Video Demo**](https://youtu.be/8qZrwkpETB4?si=DxWCpsl4_2y2mrjA)

---
## 🧭 Table of Contents
1. [Core Features](#core-features)  
2. [Technology Stack & Architecture](#technology-stack--architecture)  
3. [Firebase Services Used](#firebase-services-used)  
4. [App Architecture](#app-architecture)  
   - [Project Structure](#project-structure)  
   - [Key Architectural Decisions](#key-architectural-decisions)  
5. [Screenshots](#screenshots)  
6. [Dependencies](#dependencies)

---

## ⚙️ Core Features

### **Authentication & User Management**
- **Email & Password Authentication:**  
  Secure sign-up and login using Firebase Authentication.  

- **Google Sign-In (SSO):**  
  One-tap sign-in with Google accounts for faster onboarding.  
  Automatically creates user profiles in Firestore for new Google users.

- **Profile Management:**  
  Users can view and update their profile information, including name, email, and profile picture.

### **Book Management**
- **Book Listings:**  
  Users can create, view, update, and delete their own book listings.  
  Each listing includes title, author, price, category, condition, and images.

- **Google Books Integration:**  
  Browse millions of books from the Google Books API.  
  View detailed book information and purchase links.  
  Seamlessly integrates external content with user-generated listings.

- **Image Uploads:**  
  Upload multiple book cover images using Firebase Cloud Storage.  
  Support for camera capture and gallery selection.

### **Shopping & Transactions**
- **Shopping Cart:**  
  Add books to cart for streamlined checkout.  
  View cart totals and manage quantities.

- **Wishlist:**  
  Save books for later viewing.  
  Quick access to favorite listings.  
  Persistent across sessions.
  
  This works only for google books.

- **Transaction System:**  
  Firestore-backed purchase lifecycle management.  
  Track orders from pending to completed status.  
  View purchase history in profile.

### **Discovery & Search**
- **Dynamic Home Page:**  
  Displays available books with personalized user greetings.  
  Category-based book organization.

- **Advanced Search & Filter:**  
  Search books by title, author, or keywords.  
  Filter by category (Tech, Law, Business, Science, etc.).  
  Sort by price, date added, or relevance.

### **Notifications & Communication**
- **Push Notifications:**  
  Real-time notifications for new book listings.  
  Order status updates and transaction confirmations.  
  Firebase Cloud Messaging integration.

- **Notification Settings:**  
  Customizable notification preferences.  
  Toggle notifications by category.

### **Localization & Accessibility**
- **Multi-Language Support:**  
  Available in English, Afrikaans, and Zulu.  
  Language selection from profile settings.  
  Persists user language preference.

### **Offline Capabilities**
- **Offline Data Access:**  
  Firestore offline persistence enabled.  
  View previously loaded books without internet.  
  Automatic sync when connection restored.

---

## 🧱 Technology Stack & Architecture

| Category | Technology |
|-----------|-------------|
| **Language** | Kotlin (100%) |
| **Architecture** | MVVM (Model–View–ViewModel) |
| **UI** | XML Layouts with ViewBinding |
| **Backend** | Firebase + Google Books API |
| **Database** | Cloud Firestore (with offline persistence) |
| **Authentication** | Firebase Authentication + Google Sign-In |
| **File Storage** | Firebase Cloud Storage |
| **Push Notifications** | Firebase Cloud Messaging (FCM) |
| **External API** | Google Books API v1 |
| **Security** | Firebase App Check (Play Integrity) |
| **Async Handling** | Kotlin Coroutines |
| **Image Loading** | Glide |
| **Networking** | Retrofit + OkHttp |
| **Dependency Management** | Gradle (Kotlin DSL) |

---

## 🏗️ App Architecture

The application follows the **MVVM** pattern to separate UI logic from business logic — ensuring clean, modular, and testable code.

### 📂 Project Structure
```
com.example.bookswap
├── adapters/                   # RecyclerView adapters
│   ├── BookAdapter.kt
│   ├── WishlistAdapter.kt
│   ├── TransactionAdapter.kt
│   └── GoogleBooksAdapter.kt
├── data/
│   ├── models/                 # Data classes
│   │   ├── User.kt
│   │   ├── Book.kt
│   │   ├── Transaction.kt
│   │   └── WishlistItem.kt
│   ├── repository/             # Data operations
│   │   ├── AuthRepository.kt
│   │   ├── BookRepository.kt
│   │   ├── UserRepository.kt
│   │   ├── WishlistRepository.kt
│   │   └── GoogleBooksRepository.kt
│   ├── api/                    # API interfaces
│   │   └── GoogleBooksApi.kt
│   └── api_models/             # API response models
│       └── GoogleBooksResponse.kt
├── ui/                         # Activities and Fragments
│   ├── MainActivity.kt
│   ├── LoginActivity.kt
│   ├── RegisterActivity.kt
│   ├── HomeActivity.kt
│   ├── BookDetailActivity.kt
│   ├── ProfileActivity.kt
│   ├── CartActivity.kt
│   ├── WishlistActivity.kt
│   ├── GoogleBooksActivity.kt
│   ├── LanguageSelectionActivity.kt
│   └── NotificationSettingsActivity.kt
├── utils/                      # Utility classes
│   ├── Constants.kt
│   ├── ValidationUtils.kt
│   └── LocaleHelper.kt
├── services/
│   └── MyFirebaseMessagingService.kt  # FCM handler
├── FirebaseModule.kt           # Centralized Firebase provider
└── BookSwapApplication.kt      # Application class
```

---

### 🧠 Key Architectural Decisions

- **Centralized Firebase Initialization (`FirebaseModule.kt`):**  
  Ensures consistent Firebase instances (Auth, Firestore, Storage) across the app.  
  Prevents authentication state mismatches.

- **Repository Pattern:**  
  The data layer abstracts Firestore, Storage, and external APIs from the rest of the app.  
  Activities handle data requests without worrying about implementation details.

- **Kotlin Coroutines:**  
  All async tasks (e.g., network or Firestore queries) use coroutines for simplicity and lifecycle safety.  
  This avoids "callback hell" and integrates seamlessly with `lifecycleScope`.

- **Offline-First Design:**  
  Firestore offline persistence allows seamless operation without internet.  
  Data syncs automatically when connection is restored.

- **Multi-Language Support:**  
  Utilizes Android's resource system (`values-af`, `values-zu` folders).  
  `LocaleHelper` dynamically switches languages at runtime.  
  Persists user preference in SharedPreferences.

- **Modular API Integration:**  
  Retrofit handles Google Books API calls separately from Firebase.  
  Clean separation allows easy addition of other APIs in the future.

---

## 🔔 Push Notifications Implementation

The app uses Firebase Cloud Messaging for real-time notifications.

### Features:
- **New Book Alerts:** Notifies users when books in their preferred categories are listed
- **Order Updates:** Transaction status changes (pending → completed)
- **Welcome Messages:** Greeting new users
- **Custom Notification Channels:** Separate channels for different notification types

### Implementation:
- `MyFirebaseMessagingService.kt` handles incoming messages
- Token management for device-specific notifications
- Notification settings activity for user control

---

## 🌍 Multi-Language Support

### Supported Languages:
1. **English** (Default)
2. **Afrikaans** (af)
3. **Zulu** (zu)

### Implementation:
- Resource folders: `values/`, `values-af/`, `values-zu/`
- All user-facing strings are localized
- `LocaleHelper.kt` manages language switching
- Language preference persists across app sessions
- Settings accessible from Profile → Language Selection

---

## 📱 Offline Mode

### Capabilities:
- View previously loaded book listings
- Access cached user profile data
- Browse saved wishlist items
- View transaction history
- Automatic data synchronization when online

### Technical Details:
- Firestore offline persistence enabled globally
- Glide caches images locally
- SharedPreferences for local settings storage
- Network state monitoring for sync indicators

---

## 🖼️ Screenshots

*(Add your screenshots here once ready — e.g. Home screen, Google Books, Wishlist, Book detail, Profile, Language selection, etc.)*

---

## 📦 Dependencies

### Core Android
```kotlin
implementation("androidx.core:core-ktx:1.12.0")
implementation("androidx.appcompat:appcompat:1.6.1")
implementation("com.google.android.material:material:1.11.0")
implementation("androidx.constraintlayout:constraintlayout:2.1.4")
implementation("androidx.recyclerview:recyclerview:1.3.2")
```

### Firebase
```kotlin
implementation(platform("com.google.firebase:firebase-bom:32.7.0"))
implementation("com.google.firebase:firebase-auth-ktx")
implementation("com.google.firebase:firebase-firestore-ktx")
implementation("com.google.firebase:firebase-storage-ktx")
implementation("com.google.firebase:firebase-messaging")
implementation("com.google.firebase:firebase-appcheck")
```

### Google Services
```kotlin
implementation("com.google.android.gms:play-services-auth:21.4.0")
```

### Networking
```kotlin
implementation("com.squareup.retrofit2:retrofit:2.9.0")
implementation("com.squareup.retrofit2:converter-gson:2.9.0")
implementation("com.squareup.okhttp3:logging-interceptor:4.11.0")
```

### Image Loading
```kotlin
implementation("com.github.bumptech.glide:glide:4.16.0")
```

### Coroutines
```kotlin
implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3")
implementation("org.jetbrains.kotlinx:kotlinx-coroutines-play-services:1.7.3")
```

### UI Components
```kotlin
implementation("de.hdodenhof:circleimageview:3.1.0")
implementation("androidx.viewpager2:viewpager2:1.0.0")
```

---

## 🔐 Security Considerations

1. **API Keys:** Never commit API keys to version control. Use `local.properties`.
2. **Firestore Rules:** Update from test mode to production rules before launch.
3. **App Check:** Implement for production to prevent abuse.
4. **Input Validation:** All user inputs are validated before processing.
5. **Authentication:** Required for all sensitive operations.

---

## 🚀 Future Enhancements

- [ ] In-app messaging between buyers and sellers
- [ ] Book condition ratings and reviews
- [ ] Advanced search filters (price range, condition, location)
- [ ] Social sharing of book listings
- [ ] Payment gateway integration
- [ ] QR code generation for books
- [ ] Augmented Reality book preview
- [ ] AI-powered book recommendations

---

## 🏁 End Note

BookSwap demonstrates modern Android app development principles — blending Firebase integration, Google Cloud services, MVVM architecture, and Kotlin best practices to create a scalable, feature-rich, and user-friendly marketplace for students.

The application showcases real-world implementation of authentication (including SSO), external API integration, offline capabilities, push notifications, internationalization, and modern UI/UX patterns.

---

**Developed by:** *Nkosinathi Mabena, Barefile Lephoto, Lesego Letsapa, Lufuno Dagada*  
📧 *ST10344257@rcconnect.edu.za*  
🎓 *For University Project Use*  
📅 *2025*

---

## 📄 License

This project is developed for educational purposes as part of university coursework.

---

## 🙏 Acknowledgments

- Firebase for backend infrastructure
- Google Books API for book data
- Android development community for invaluable resources
- University faculty for guidance and support
