# 🎶 Music-Inspired Outfit Recommender

This project analyzes the color schemes of album covers from a user's top Spotify tracks and uses these colors to recommend outfits through the ShopStyle API. The application combines colors from album art with current season and gender preferences to deliver tailored fashion recommendations.

## 📑 Table of Contents

1. [📚 Libraries Used](#-libraries-used)
2. ⚙️ Setup
   - [🎧 Spotify API](#-spotify-api)
   - [🛍️ ShopStyle API](#-shopstyle-api)
3. [🚀 Usage](#-usage)
4. [🛠️ Project Workflow](#-project-workflow)
5. [🔧 Sorting Options for Recommendations](#-sorting-options-for-recommendations)
6. [💻 Example Code Structure](#-example-code-structure)
7. [✨ Future Improvements](#-future-improvements)



------

### 📚 Libraries Used

Here are the key libraries used in this project, with brief descriptions:

- **Spotipy**: For interacting with the Spotify API to fetch user data and top tracks.
- **Requests**: To handle API requests to the ShopStyle API.
- **Numpy**: For handling arrays and numerical data.
- **CV2 (OpenCV)**: Used to download album images and handle color processing.
- **Scikit-learn (KMeans)**: For clustering colors from album cover images.
- **Matplotlib**: For visualizing album cover color schemes as color bars.
- **Pandas**: To structure data (optional, used in data processing).
- **IPython.display**: For displaying images inline (useful in Jupyter Notebook environments).

- **Jupyter Notebook**: The place to run the code.

  

Install these libraries via pip if necessary:

```
pip install spotipy requests numpy opencv-python scikit-learn matplotlib pandas jupyter
```

### ⚙️ Setup

#### 🎧 Spotify API (The way we learn on Class06-APIs)

1. **Create a Spotify Developer Account**: Go to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/) and create a new application to get the `client_id` and `client_secret`.

2. **Configure Redirect URI**: Add a redirect URI in your Spotify developer dashboard that matches the redirect URI used in the project.

3. **Save Spotify Credentials**: Save your credentials in a JSON file named `spotify_keys.json` with the following format:

   ```
   {
       "username": "YOUR_USER_NAME"
       "client_id": "YOUR_SPOTIFY_CLIENT_ID",
       "client_secret": "YOUR_SPOTIFY_CLIENT_SECRET"
       "redirect": "https://googole.com"(your own Redirect URIs in Spotify Developer Account Setting.)
   }
   ```

#### 🛍️ ShopStyle API

1. **Create a ShopStyle Collective Account**: Sign up at [ShopStyle Collective](https://support.collectivevoice.com/hc/en-us) and create a new application.
2. **Retrieve API Key**: Once finish sign-up, you’ll receive a UID/API key in your Account Profile.
3. **Save ShopStyle API Key**: Save the API Key in a txt file under your file folder.

------

### 🚀 Usage

1. **Import and Configure Libraries**: Ensure all necessary libraries are installed and configured.
2. **Run the Script**: Use a Jupyter Notebook to run each function interactively.
3. **View Outfit Recommendations**: The code will display album colors as bars and output clothing items based on your own top three songs in the playlist and based on color combinations.

### 🛠️ Project Workflow

1. **🎵 Fetch Top Songs from Spotify**:
   - Using Spotipy, the script fetches the user's top three Spotify tracks. For each track, it retrieves the album cover image URL.
2. **🎨 Process Album Cover Colors** (Those code is from [Spotify API Color Sorter]([Spotify API Color Sorter. by Carey Crooks | by Carey Crooks | Medium](https://medium.com/@clcrooks/spotify-api-color-sorter-6cb935b9a8fd))) :
   - Download and process each album cover image using OpenCV.
   - Apply KMeans clustering to extract the top three colors from each album cover.
   - Display these colors as a color bar for visual reference.
3. **🎨 Convert Colors to Fashion-Friendly Names**:
   - The RGB values are mapped to commonly used fashion colors (e.g., "black," "white," "gray") to make the color schemes more applicable to clothing.
4. **🛍️ Fetch Outfits from ShopStyle API**:
   - Search for clothing items matching the color scheme of each album cover, filtering by season and gender.
   - If no items are found, the code defaults to searching for individual colors or more general fashion terms (like "neutral tones") to ensure relevant results.
5. **📸 Display Recommendations**:
   - The recommended outfits are displayed with images, names, prices, brands, and links to the ShopStyle website.

------

### 🔧 Sorting Options for Recommendations

When calling the ShopStyle API, you can specify how to sort the outfit recommendations by passing a `sort_by` parameter to `get_outfit_suggestions`. The following options are available:

- **"popularity"** – Sorts by the most popular items (default).
- **"price"** – Sorts by price from low to high.
- **"price_desc"** – Sorts by price from high to low.
- **"new"** – Sorts by the latest arrivals.
- **"relevance"** – Sorts by relevance based on the search term.

Example usage:

```
# Display outfits sorted by price (low to high)
display_top_songs_colors_and_outfits("women", top_songs_colors, sort_by="price")

# Display outfits sorted by new arrivals
display_top_songs_colors_and_outfits("women", top_songs_colors, sort_by="new")
```

------

### 💻 Example Code Structure

Below is a sample structure of the main functions in the script:

- **get_top_songs_colors**: Fetches Spotify tracks (songs) and extracts album colors.
- **get_outfit_suggestions**: Queries ShopStyle API based on combined album colors, gender, current season and sorting options.
- **display_outfits**: Displays the outfit recommendations or fetches a sample if no matches are found.

This project combines music and fashion by translating album art colors into personalized outfit recommendations. 

------

### ✨ Future Improvements

While the current functionality provides a basic music-inspired outfit recommendation, there are some areas for improvement:

- **Gender Filtering Accuracy**: Occasionally, men’s clothing items appear in women’s outfit recommendations. Enhancing the gender filtering in API calls or applying additional filters to item attributes could improve the accuracy.
- **Color and Style Matching**: Currently, outfits are recommended based solely on album color matching, which can lead to generic suggestions. A more nuanced approach would incorporate the style and mood of the song (e.g., a vibrant song could suggest casual or sporty styles, while a mellow song might suggest formal or relaxed styles). Future improvements could analyze audio features from Spotify (like energy, tempo, and mood) and combine them with colors for more contextually relevant fashion recommendations.

These enhancements would add depth and personalization, making the recommendations more aligned with both the music’s style and the listener’s preferences.