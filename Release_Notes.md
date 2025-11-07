# BookSwap v1.0.0 - POE Release Notes
**Date:** November 7, 2025

This is the first major release of the BookSwap application for the 2025 POE submission. This version transitions the project from a base prototype to a fully-featured, cloud-based mobile application with several innovative features.

## 🚀 New Features & Innovations

This release introduces advanced, POE-specific functionality:

* **Google Sign-In (SSO):**
    * Users can now sign up and log in instantly using their existing Google accounts, in addition to the standard email/password method.

* **Real-time Push Notifications:**
    * Implemented a server-side back-end using **Firebase Cloud Functions (Node.js)**.
    * **Sellers** receive an instant push notification when their book is sold.
    * **Buyers** receive an instant "Order Confirmed" push notification upon checkout.
    * **Topic Subscriptions:** Users can subscribe to notifications for new books listed in their favorite categories (e.g., "TECH", "LAW").
    * **Admin Announcements:** Includes an `ANNOUNCEMENTS` topic for an admin to send general notifications to all users.

* **Multi-Language Support:**
    * The app is now fully localized for **English**, **Afrikaans**, **isiZulu**, and **Setswana**.
    * A new settings page allows users to switch their language, and the entire app UI updates instantly (using `AppCompatDelegate`).

* **Google Books API & Wishlist:**
    * Integrated the Google Books API (using Retrofit) to allow users to search the entire Google Books catalog.
    * Users can add books from Google Books to a personal "Wishlist," which is saved to their user profile in Firestore.

* **Offline Mode with Sync:**
    * Enabled Firestore's built-in offline persistence.
    * The app automatically caches all fetched data (books, user profiles, cart, etc.).
    * Users can browse the app, view listings, and manage their profile even when offline. Any changes are automatically synced when the connection is restored.



## 🐞 Bug Fixes & Improvements
* Fixed a critical crash related to `String` vs. `Double` data types for book prices.
* Resolved a `FAILED_PRECONDITION` error by implementing the required composite indexes in Firestore for book and transaction queries.
* Fixed a fatal app startup crash (`NullPointerException`) by moving language-switching logic from `attachBaseContext` to the `Application.onCreate` method.
* Resolved multiple Cloud Function deployment errors by upgrading to v2 syntax and setting the correct IAM (permissions) roles in the Google Cloud project.
