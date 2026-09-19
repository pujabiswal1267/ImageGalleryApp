# ImageGalleryApp

A modern, production-grade React Native & TypeScript cross-platform mobile application featuring photography discovery, persistent authentication, offline favorites, image downloading, and profile management.

---

## 1. Project Name
**ImageGalleryApp** (`react-native-image-gallery`)

---

## 2. Project Description
**ImageGalleryApp** is a photography exploration and curation application designed and engineered to meet all requirements of the React Native Intern Assignment. Built with React Native, TypeScript, Expo SDK 57, and React Navigation 7, the application features an **ultra-modern Dark Studio & Glassmorphism** design language inspired by world-class platforms like Unsplash Pro, Apple Photos, and VSCO.

The app supports comprehensive local-first authentication (8 validated fields, session persistence), curated photography grids with case-insensitive search and author filters (A–M, N–Z), infinite scrolling, pull-to-refresh, real-time persistent favorites, high-resolution full-screen viewing, native/web gallery image downloading, and full user profile editing.

---

## 3. Features
- **Local-First Authentication**:
  - Registration with 8 rigorously validated fields (Full Name, Email, Gender, 10-digit Mobile Number, Address, City Dropdown, Password, Confirm Password).
  - Login with credential verification against stored records in `@react-native-async-storage/async-storage`.
  - Persistent login session that automatically restores upon app launch.
  - Safe Logout flow with custom modal confirmation.
- **Curated Image Gallery**:
  - Dynamic integration with the Picsum Photos API (`https://picsum.photos/v2/list`).
  - 2-Column responsive masonry grid with proportional aspect ratios (1.15).
  - Infinite scroll pagination (`onEndReached`) loading 50 images per batch with deduplication.
  - Pull-to-refresh (`RefreshControl`) to fetch the freshest photography.
  - Instant Favorite toggle with animated glowing glass badges.
- **Search & Filtering**:
  - Real-time debounced search by author name (case-insensitive).
  - Segmented author filters: `All Photos`, `Author A–M`, `Author N–Z`.
  - Simultaneous search and filter combinations with live photo counters.
- **Persistent Favorites**:
  - Dedicated Favorites screen with a 2-column grid.
  - In-favorites case-insensitive search.
  - Immediate add/remove toggle and batch "Clear All" modal.
  - Exact empty state message: `"No favorite images yet."`.
  - Fully persisted to AsyncStorage.
- **Image Details & Full-Screen Viewer**:
  - High-resolution image preview with author info and technical specifications (ID, Quality, Source).
  - Full-screen viewer modal with pan-fit zoom scaling, loading spinners, and network error retry handlers.
- **Real Image Download to Gallery**:
  - **Web**: Direct blob-based anchor download to user's local Downloads directory.
  - **Mobile (iOS & Android)**: Uses `expo-file-system` and `expo-media-library` with permissions handling, saving directly to the user's camera roll/gallery.
- **Profile Management**:
  - Comprehensive profile view displaying Full Name, Email, Mobile Number, Gender, Address, City, and Member Since date.
  - Full Edit Profile functionality with real-time field validation, immediate AsyncStorage persistence, and global state synchronization.
- **Aesthetic Excellence**:
  - Complete Dark Studio & Glassmorphism theme (`#0A0E1A` obsidian base, `#121829` glass cards, `#6366F1` electric indigo accents).
  - Zero deprecated `pointerEvents` or `shadow*` warnings (`Pressable` and `boxShadow` with `Platform.select`).

---

## 4. Technologies
- **Core**: React Native 0.86.3, React 19.2.3, Expo SDK 57 (~57.0.24)
- **Language**: TypeScript 6.0 (~6.0.3)
- **Navigation**: React Navigation 7 (`@react-navigation/native`, `@react-navigation/native-stack`, `@react-navigation/bottom-tabs`)
- **State Management**: React Context API (`AuthContext`, `FavoritesContext`) + Custom Hooks
- **Persistence**: `@react-native-async-storage/async-storage` 2.2.0
- **Device Capabilities**: `expo-file-system` (~57.0.7), `expo-media-library` (~57.0.5)
- **Icons**: `@expo/vector-icons` (Ionicons)
- **Safe Area**: `react-native-safe-area-context` (~5.7.0)

---

## 5. API Used
- **Picsum Photos API**: `https://picsum.photos/v2/list?page={page}&limit={limit}`
  - Dedicated service layer: `src/services/imageService.ts`
  - Strongly-typed `GalleryImage` interface (`id`, `author`, `width`, `height`, `url`, `download_url`)
  - Fast thumbnail generator: `https://picsum.photos/id/{id}/{width}/{height}`

---

## 6. Installation

Ensure you have [Node.js](https://nodejs.org/) (v18+) and [npm](https://www.npmjs.com/) installed.

```bash
# Clone or navigate to the project directory
cd react-native-image-gallery

# Install dependencies
npm install
```

---

## 7. Running the Application

```bash
# Start Expo development server (interactive menu)
npm run start

# Launch directly in Web browser
npm run web

# Run on Android emulator / device
npm run android

# Run on iOS simulator (macOS required)
npm run ios
```

The application is hosted by Metro on `http://localhost:8081`.

---

## 8. Folder Structure

```
react-native-image-gallery/
├── App.tsx                        # Main application root with providers
├── app.json                       # Expo configuration and permissions
├── package.json                   # Project dependencies and scripts
├── tsconfig.json                  # TypeScript compiler options
├── README.md                      # Complete project documentation
└── src/
    ├── components/                # Reusable presentation components
    │   ├── CityDropdown.tsx       # Searchable modal city picker
    │   ├── CustomButton.tsx       # Universal button with Pressable & variants
    │   ├── CustomInput.tsx        # Text input with validation and eye toggle
    │   ├── FilterTabs.tsx         # Segmented filter pills with counts
    │   ├── GenderRadio.tsx        # Radio pills for Male/Female/Other
    │   ├── ImageCard.tsx          # 2-column photography card with heart toggle
    │   └── SearchBar.tsx          # Translucent glass search capsule
    ├── context/                   # Centralized global state providers
    │   ├── AuthContext.tsx        # Auth state (register, login, session, user)
    │   └── FavoritesContext.tsx   # Centralized favorites state & actions
    ├── hooks/                     # Custom React hooks
    │   ├── useAuth.ts             # Hook to access AuthContext
    │   ├── useDebounce.ts         # Hook for debouncing search inputs
    │   └── useFavorites.ts        # Hook to access FavoritesContext
    ├── navigation/                # React Navigation configuration
    │   ├── AuthNavigator.tsx      # Stack for Login and Register screens
    │   ├── MainNavigator.tsx      # Bottom tabs (Home, Favorites, Profile) + Stacks
    │   └── RootNavigator.tsx      # Auth vs. Main conditional routing
    ├── screens/                   # Application screens
    │   ├── auth/
    │   │   ├── LoginScreen.tsx    # User login screen
    │   │   └── RegisterScreen.tsx # User registration screen (8 fields)
    │   └── main/
    │       ├── FavoritesScreen.tsx       # Favorites gallery with search & empty state
    │       ├── FullScreenImageScreen.tsx # Immersive full-screen image viewer
    │       ├── HomeScreen.tsx            # Main photo feed with search, filter, infinite scroll
    │       ├── ImageDetailsScreen.tsx    # Detailed photo view with download & specs
    │       ├── ImageViewerScreen.tsx     # Aliased export of FullScreenImageScreen
    │       └── ProfileScreen.tsx         # User profile and live profile editor
    ├── services/                  # Network and native device services
    │   ├── imageDownloadService.ts # Real image downloading (Web & Native)
    │   └── imageService.ts        # Picsum API requests and thumbnail helpers
    ├── storage/                   # Local persistence layer
    │   └── storageService.ts      # AsyncStorage CRUD operations
    ├── types/                     # TypeScript declarations
    │   ├── auth.ts                # User, session, and auth form types
    │   ├── image.ts               # Picsum API and filter types
    │   └── navigation.ts          # React Navigation stack & tab param lists
    └── utils/                     # Constants and validation helpers
        ├── constants.ts           # Design tokens, storage keys, city list
        └── validation.ts          # Pure form validators (email, mobile, edit, etc.)
```

---

## 9. Architecture
The project strictly implements a **Separation of Concerns** pattern:
- **Presentation Layer (`src/components`, `src/screens`)**: Pure UI focused on rendering state, managing user interactions, and visual animations.
- **State & Domain Layer (`src/context`, `src/hooks`)**: Centralized business logic without prop-drilling.
- **Persistence Layer (`src/storage`)**: Encapsulated AsyncStorage operations with typed serialization and error boundaries.
- **Service Layer (`src/services`)**: Decoupled HTTP API integrations and native file downloads.
- **Validation Layer (`src/utils/validation.ts`)**: Pure, testable functions returning validation states and user-friendly error messages.

---

## 10. State Management
Centralized state is handled via React's Context API and custom hooks:
1. **`AuthContext` (`useAuth`)**:
   - Manages `user: User | null`, `session: AuthSession | null`, and `isLoading: boolean`.
   - Exposes `register()`, `login()`, `logout()`, and `updateUser()`.
2. **`FavoritesContext` (`useFavorites`)**:
   - Manages `favorites: GalleryImage[]`.
   - Exposes `isFavorite(id)`, `addFavorite(image)`, `removeFavorite(id)`, `toggleFavorite(image)`, and `clearFavorites()`.

---

## 11. AsyncStorage
Local persistence keys managed in `src/utils/constants.ts`:
- `@app_user`: Stores registered `User` profile data.
- `@app_session`: Stores active `AuthSession` with authentication flag and login timestamp.
- `@app_favorites`: Stores array of favorited `GalleryImage` objects.

All reads and writes use safe JSON serialization with defensive `try...catch` blocks in `src/storage/storageService.ts`.

---

## 12. Authentication Flow
```
App Launch
  │
  ├─ Check AsyncStorage (@app_session)
  │     │
  │     ├─ Authenticated ──> RootNavigator renders MainNavigator (Gallery/Tabs)
  │     │
  │     └─ Not Authenticated ──> RootNavigator renders AuthNavigator (Login/Register)
  │
  ├─ Registration: Validates 8 fields -> Saves user to @app_user -> Navigates to Login
  │
  ├─ Login: Matches credentials against @app_user -> Writes session to @app_session -> Auto-navigates to Main
  │
  └─ Logout: Clears @app_session -> Keeps @app_user intact -> Auto-redirects to Login
```

---

## 13. Image Gallery Flow
1. `HomeScreen` mounts and invokes `imageService.fetchImages(page=1, limit=50)`.
2. Returned images are deduplicated by `id` to prevent duplicates.
3. Images render in a 2-column `FlatList`.
4. Pull-to-refresh resets `page=1` and refreshes the collection.
5. Scrolling down triggers `onEndReached` (threshold `0.4`), fetching `page + 1` seamlessly.

---

## 14. Search and Filter
- **Search**: Real-time text search debounced by 300ms (`useDebounce`) matching author names case-insensitively (`author.toLowerCase().includes(query)`).
- **Filter**:
  - `ALL`: Displays all fetched photos.
  - `A_M`: First character of author name between `A` and `M`.
  - `N_Z`: First character of author name between `N` and `Z`.
- **Combination**: Both search and filter criteria are applied simultaneously.

---

## 15. Pagination
- Pagination is implemented using Picsum Photos' `?page={page}&limit=50` endpoint.
- Handled with FlatList's `onEndReached` with defensive checks against duplicate in-flight requests (`isFetchingMore`, `isLoadingInitial`).
- Shows an inline footer spinner when fetching subsequent pages.

---

## 16. Favorites Persistence
- Tapping the heart icon on any card immediately executes `toggleFavorite(image)`.
- Updates centralized `favorites` in memory and persists to `@app_favorites` in AsyncStorage.
- Saved photos remain intact across app restart, navigation, and pull-to-refresh.
- Favorites screen features in-memory search and an explicit empty state: `"No favorite images yet."`.

---

## 17. Image Download
- **Web**: Fetches image as a Blob, generates an Object URL, and triggers an anchor download to user's local Downloads directory.
- **Mobile (iOS/Android)**:
  1. Requests device gallery permissions (`expo-media-library`).
  2. Downloads photo to local cache directory (`expo-file-system`).
  3. Saves asset directly to device Photo Library (`MediaLibrary.createAssetAsync`).
  4. Displays feedback modal confirming download or detailing permission issues.

---

## 18. Profile Management
- `ProfileScreen` displays user details: Full Name, Email, Mobile Number, Gender, Address, City, Member Since.
- **Edit Profile**:
  - Tap "Edit" to launch the edit modal.
  - Allows editing Full Name, Mobile Number, Gender, Address, and City. Email is non-editable.
  - Validates fields via `validateEditProfileForm`.
  - Calls `updateUser()` to update AsyncStorage and centralized context state simultaneously.
  - Changes reflect across the application immediately.

---

## 19. Assumptions
1. Single user account registered locally on the device (per assignment specifications).
2. Email address serves as the primary unique account identifier and cannot be modified.
3. Mobile numbers are validated according to the standard 10-digit format.
4. On Web desktop platforms, image downloads route directly to the browser's default Downloads folder.

---

## 20. Libraries Used
| Package | Version | Purpose |
| :--- | :--- | :--- |
| `expo` | ~57.0.24 | Core application runtime and SDK |
| `react` & `react-dom` | 19.2.3 | UI component library |
| `react-native` | 0.86.3 | Mobile framework |
| `@react-navigation/native` | ^7.4.1 | Navigation container |
| `@react-navigation/native-stack` | ^7.19.2 | Stack navigator |
| `@react-navigation/bottom-tabs` | ^7.19.2 | Bottom tab navigator |
| `@react-native-async-storage/async-storage` | 2.2.0 | Offline persistence engine |
| `expo-file-system` | ~57.0.7 | Local device file downloading |
| `expo-media-library` | ~57.0.5 | Native photo gallery asset creation |
| `@expo/vector-icons` | ^15.0.2 | Ionicons icon set |
| `react-native-safe-area-context` | ~5.7.0 | Display notch & edge insets |
| `react-native-screens` | ~4.26.0 | Native screen optimization |

---

## 21. Testing Instructions

### Automated Unit Tests
Run the project's standalone unit test suite:
```bash
node scratch/full-test-suite.js
```
*Executes 29/29 assertions validating form validation, login matching, session storage, search/filter algorithms, and favorites toggling.*

### Type Checking & Bundling
```bash
# Verify zero TypeScript errors
npx tsc --noEmit

# Verify clean Web export bundle
npx expo export -p web --dev
```

### Manual Verification Checklist
1. **Registration**: Try invalid fields (blank, short password, 8-digit mobile) -> errors highlight. Submit valid data -> success modal displays and redirects to Login.
2. **Login**: Attempt incorrect password -> error banner appears. Enter registered credentials -> navigates to Gallery.
3. **Session Persistence**: Refresh browser or restart app -> remains logged into Gallery without redirecting to Login.
4. **Gallery Feed**: 2-column grid renders photos. Scroll to bottom -> next 50 images load. Pull to refresh -> resets and refreshes.
5. **Search & Filter**: Type an author name -> grid filters case-insensitively. Select `Author A–M` or `Author N–Z` -> grid filters accordingly.
6. **Favorites**: Tap heart on an image card -> heart fills red with glow. Open "Favorites" tab -> photo appears. Search within favorites -> matches author.
7. **Image Details**: Tap photo card -> details screen opens with photographer info, photo ID, and specs.
8. **Full Screen**: Tap photo on details screen -> full-screen modal opens with pan-fit display and back button.
9. **Image Download**: Tap "Download to Gallery" -> photo is downloaded and saved to disk/gallery with success modal.
10. **Edit Profile**: Open "Profile" tab -> tap "Edit" -> change Name/City/Mobile -> Save -> profile updates instantly in UI and storage.
11. **Logout**: Tap "Log Out" -> confirm modal -> returns to Login screen. Gallery screens become inaccessible until logged back in.
